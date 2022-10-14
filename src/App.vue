<template>
  <div class="container">
    <MyHeader  @toggle-add-task ="toggleAddTask" title = "Task Tracker" :showAddTask="showAddTask"/>
    <div v-if="showAddTask">
    <AddTask @add-task="addTask" />
  </div>
    <MyTask  @toggle-reminder="toggleReminder" @data-text="dataText"   @delete-task="deleteTask" :tasks='tasks' />
    
  </div>
</template>

<script>
  import MyHeader from './components/MyHeader'
  import MyTask from './components/MyTask'
  import AddTask from './components/AddTask.vue'

export default {
  
  name: 'App',
  components: {
    MyHeader,
    MyTask,
    AddTask
},
  data(){
    return{
      tasks:[],
      showAddTask :false
    }

  },
 
  methods:{
     addTask(task){
       this.tasks = [...this.tasks,task]
     },

    deleteTask(id){
      if(confirm('Are you sure'))
      this.tasks = this.tasks.filter((task)=>  task.id != id)
    },
    toggleReminder(id){
   this.tasks.find(el => el.id === id ? el.reminder = !el.reminder :'' )
  },
  dataText(id){
    this.tasks.find(el => id === el.id ? console.log(el.text) :'' )

  },
  toggleAddTask(){
    this.showAddTask = !this.showAddTask
  },
  async fetchTask(){
     const res = await fetch('http://localhost:5000/tasks')
     const data = await res.json()
     console.log(data,'fjkjkljkljlk')
     return data
  }
    
  },
 async created(){
   this.tasks = await this.fetchTask()
  
  },
}
</script>


<!-- STYLE -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.container{
  border: 1px solid black;
}

.btn{
  display: inline-block;
  background: rgb(39, 39, 39);
  color: white;
  border: none;
padding: 10px 20px;
margin: 5px;
border-radius: 5px;
cursor: pointer;
text-decoration: none;font-size: 15px;
font-family: inherit ;
}



</style>
