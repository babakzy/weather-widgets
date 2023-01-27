<script setup>
import wdiget1 from './components/widget1.vue'
import wdiget2 from './components/widget2.vue'
import wdiget3 from './components/widget3.vue'
import getLocation from './use/geolocation'
import { onMounted } from 'vue';
import { ref } from 'vue';
let temperatureData = ref(0);
let descriptionData = ref(" ");
let cityData = ref(" ");

function mycallback(position) {
  alert("s")
console.log(position)
}
function showError(position) {
  alert("s")
console.log('11')
}
onMounted(() => {
 // getLocation(mycallback());
  navigator.geolocation.getCurrentPosition(mycallback, showError);
  fetch("https://api.openweathermap.org/data/2.5/weather?lat=38.0797&lon=46.3002&appid=97c3dcd58e47ab9b00baac7d422371d3")
    .then(x => x.text())
    .then((data) => {
      data = JSON.parse(data)
      temperatureData.value = (data.main.temp - 273.15).toFixed() + '°C' // Convert from Kelvin to Celsius
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
    <div class="container">
      <div class="column">  <wdiget1 :temperature="temperatureData" :description="descriptionData" :city="cityData" /></div>
      <div class="column">  <wdiget2 :temperature="temperatureData" :description="descriptionData" :city="cityData" /></div>.
      <div class="column">  <wdiget3 :temperature="temperatureData" :description="descriptionData" :city="cityData" /></div>
    </div>
  
   
  </main>
</template>

<style scoped>
.container{
  display: flex;
  flex-wrap: nowrap;
}
.column{

  width: 50%;
  padding:50px;
}
main {
  margin: 70px;
}
.logo {
  padding-top: 70px;
  display: block;
  margin: auto;
}
</style>
