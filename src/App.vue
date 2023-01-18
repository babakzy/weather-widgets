<script setup>
import wdiget1 from './components/wdiget1.vue'
import { onMounted } from 'vue';
import { ref } from 'vue';
let temperatureData = ref(0);
let descriptionData = ref(" ");
let cityData = ref(" ");
onMounted(() => {
  fetch("https://api.openweathermap.org/data/2.5/weather?lat=38.0797&lon=46.3002&appid=97c3dcd58e47ab9b00baac7d422371d3")
    .then(x => x.text())
    .then((data) => {
      data = JSON.parse(data)
      console.log(data)
      temperatureData.value = data.main.temp
      descriptionData.value = data.weather[0].description
      cityData.value = data.sys.country + ', ' + data.name
    })

})

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="70" height="70" />
  </header>
  <main>
    <wdiget1 :temperature="temperatureData" :description="descriptionData" :city="cityData" />
   
  </main>
</template>

<style scoped>

main {
  margin: 70px;
}
.logo {
  padding-top: 70px;
  display: block;
  margin: auto;
}
</style>
