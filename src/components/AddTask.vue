<template>
    <form @submit="onSubmit" class="add-form">
    <div class="form-control">
        <label for="">Taask</label>
        <input class="input-text" v-model="text" type="text" name="text" placeholder="Add Task"> 
    </div>
    <div class="form-control">
        <label for="">Day & Time</label>
        <input  class="input-text" v-model="day" type="text" name="day" placeholder="Add date &  time"> 
    </div>
    <div class="form-control form-control-check">
        <label for="">Set Reminder</label>
        <input type="checkbox" v-model="reminder" name="reminder" placeholder="reminder"> 
    </div>
    <div class="form-control form-control-check">
        <input type="submit" name="Save Task" class="btn btn-add"> 
    </div>
    </form>
</template>


<script>
export default{
    name:'AddTask',
    data (){
      return{ 
        text:'dzedzd',
        day:'',
        reminder:false
    }
    },
    methods:{
        onSubmit(e){
          e.preventDefault()
          if(!this.text){
            alert('please add a task')
            return
          }

          const newTask = {
              id : Math.floor(Math.random()  * 100000),
              text:this.text,
              day:this.day,
              reminder:this.reminder
          }
          console.log(newTask)
          this.$emit('add-task',newTask)
         
          this.text = 'dzedzd',
          this.day = '',
           this.reminder = false
        } 
    }
}
</script>


<style scoped>

.add-form{
    margin: 0 20px 2em 20px;
    background-color: rgba(255, 255, 255, 0.968);
    padding: 0.5em 1em;
}

.form-control{
    display: flex;
    flex-direction: column;
    gap: .5em;
    margin: 1em 0;
}

.form-control:nth-child(3){
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-top: 1.5em;
}
.input-text{
    padding: .8em .5em;
}
.btn-add{
    width: 100%;
}


</style>