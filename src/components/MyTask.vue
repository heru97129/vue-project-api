<template>
   <div class="container-task">
  <div v-for="task in tasks" :key="task.id">
    <SingleTask @toggle-reminder="$emit('toggle-reminder',task.id)" @data-text="$emit('data-text',task.id)"  @delete-task ="$emit('delete-task',task.id)"  :task="task"/> 
  </div>
</div>
</template>

<script>
import SingleTask from './SingleTask.vue'
export default {
    name:'MyTask',
    props:{
        tasks:Array
    },
    components :{
       SingleTask 
    },
    emit:['delete-task','toggle-reminder','data-text']
}
</script>

<style scoped>

.container-task{
  padding: 0 20px;
}

</style>