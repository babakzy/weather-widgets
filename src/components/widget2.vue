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
  border: 3px solid rgb(0, 0, 0);
  padding: 10px;
  display:flex;
  max-width: 400px;
  flex-wrap: wrap;
  border-radius: 4px;
  align-items: center;
}
.temperature{
  flex-grow: 1;
  text-align: center;
}
.info{
  background-color: rgb(164, 183, 207);
  padding: 14px;
  border-radius: 8px;
  flex-grow: 3;
  text-transform: capitalize;
  
}
.info h2,h3{
line-height: 0;
}
</style>
