<template>
    <div @dblclick="$emit('toggle-reminder',task.id)"  @click="$emit('data-text',task.id)"  :class="[ task.reminder ? 'reminder' : '' ,'task']">
<h3>{{task.text}}
 <i @click="$emit('delete-task',task.id)" class="fas fa-times"></i> 

</h3>

<p>{{task.day}}</p>
</div>
</template>

<script>
export default {
    name:'SingleTask',
    props:{
        task:Object
    },
 
}
</script>


<style scoped>
.fa-times{
    color: red;
}
 .task{
   background-color: #f4f4f4;
   margin: 5px;
   padding: 10px 20px;
 }
 h3{
    display: flex;
    justify-content: space-between;
    align-items: center;
 }

 .reminder{
  position: relative;
}

.reminder::after{
    content: '';
    position: absolute;
    left: 0;
    top: 0;
    background-color: green;
    width: 2%;
    height: 100%;
    z-index: 5475554;

}

</style>