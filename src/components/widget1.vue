<script setup>
const props = defineProps({
  temperature:Number,
  description:String,
  city:String
})
</script>

<template>
  <div class="widget-container">
    <div class="temperature"><h1>{{ props.temperature }}</h1></div>
    <div class="info"><h2>{{ props.description }}</h2>
    <p>{{props.city}}</p>
  </div>
  </div>
</template>

<style scoped>
.widget-container{
  border: 2px solid rgb(47, 29, 90);
  padding: 10px;
  display:flex;
  max-width: 400px;
  flex-wrap: wrap;
  border-radius: 8px;
  align-items: center;
}
.temperature{
  flex-grow: 1;
  text-align: center;
  padding: 20px;
}
.info{
  background-color: rgb(212, 212, 212);
  padding: 14px;
  border-radius: 8px;
  flex-grow: 3;
  text-transform: capitalize;
  
}
.info h2,h3{
line-height: 0;
}
</style>
