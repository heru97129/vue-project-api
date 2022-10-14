<template>
    <header>
        <h1>{{title}}</h1>
        <MyButton @btn-click="$emit('toggle-add-task')"  :text="showAddTask ?'Close':'Add task '" :color="showAddTask ? 'red':'green'" />
    </header>
</template>


<script>
import MyButton from './MyButton.vue'
export default {
    name: "MyHeader",
    props: {
        title: String,
        showAddTask : Boolean
    },
    components: {
        MyButton
    }
}
</script>


<style scoped>
header{
   display: flex;
   justify-content: space-between;
   align-items: center;
   margin-bottom: 20px; 
   padding: 0 20px;
}

</style>