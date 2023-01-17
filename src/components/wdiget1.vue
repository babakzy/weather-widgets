<script setup>
defineProps({
  msg: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="widget-container">
    <div class="temperature"><h1>32</h1></div>
    <div class="info"><h2>broken clouds</h2>
    <p>IR, Tabriz</p>
  </div>
  </div>
</template>

<style scoped>
.widget-container{
  border: 1px solid gray;
  padding: 10px;
  display:flex;
  width: 400px;
}
.temperature{
  flex-grow: 1;
  text-align: center;
}
.info{
  background-color: burlywood;
  flex-grow: 3;
  
}
</style>
