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
    //  ajouter des taches 
    async addTask(task){
      const res = await fetch('api/tasks',{
        method:'POST',
        headers :{
          'content-type' :'application/json',
        },
        body: JSON.stringify(task)

      })
      
      const data = await res.json()

       this.tasks = [...this.tasks,data]
     },

    //   suprimer des taches 
 async  deleteTask(id){
      if(confirm('Are you sure')){
        const res = await fetch(`api/tasks/${id}`,{
          method:'DELETE',

        })
        res.status == 200 ? (this.tasks = this.tasks.filter((task)=>  task.id != id)) : alert('error delete task')
      
      }
    },


    //   toggle des taches  des taches 

   async toggleReminder(id){
    const taskToggle = await this.fetchTask(id)
    const upTask = {...taskToggle, reminder: !taskToggle.reminder}
console.log(upTask)
     const res = await fetch(`api/tasks/${id}`,{
      method:'PUT',
      headers:{
        'Content-type' : 'application/json',
      },
      body:JSON.stringify(upTask)
 
     })   
     const data = await res.json()
     this.tasks = this.tasks.map((task)=>  task.id === id ? {...task,reminder: data.reminder} : task)
     },
      

  dataText(id){
    this.tasks.find(el => id === el.id ? console.log(el.text) :'' )

  },
toggleAddTask(){
 

    this.showAddTask = !this.showAddTask
  },

  //  récupére les donnée dans l'api 
  async fetchTasks(){
     const res = await fetch(`api/tasks`)
     const data = await res.json()
     console.log(data,'fjkjkljkljlk')
     return data
  },
  async fetchTask(id){
     const res = await fetch(`api/tasks/${id}`)
     const data = await res.json()
     console.log(data,'fjkjkljkljlk')
     return data
  }
    
  },
 async created(){
   this.tasks = await this.fetchTasks()
  
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
