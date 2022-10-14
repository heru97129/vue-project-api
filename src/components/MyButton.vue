<template>
    <button @click="move()"  :style="{backgroundColor:color}" class="btn">{{text}}</button>
</template>


<script>

export default {
   name:'MyButton',
   props:{
    text: String,
    color:String
   },
   methods :{
   move(){
    this.$emit('btn-click')
   }
}
}
</script>