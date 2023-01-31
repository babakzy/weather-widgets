<script setup>
import wdiget1 from './components/widget1.vue'
import wdiget2 from './components/widget2.vue'
import wdiget3 from './components/widget3.vue'
import getLocation from './use/geolocation'
import { onMounted } from 'vue';
import { onBeforeMount } from 'vue';
import { ref , watch } from 'vue';
let temperatureData = ref(0);
let descriptionData = ref(" ");
let cityData = ref(" ");
let lat = ref("");
let lon = ref("");
let temperatureUnit = ref("");

onBeforeMount(() => {

})

onMounted(() => {

  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(locationSuccessCallback, locationShowError);
    console.log('1 navigator.geolocation onMounted')
  } else {
    alert("Geolocation is not supported by this browser.");
  }  
  
})

watch (temperatureUnit,()=>{
  console.log(temperatureUnit.value)
  if (temperatureUnit.value == "kelvin"){
    alert(temperatureData.value)
    temperatureData.value = (Number(temperatureData.value) - 273.15).toFixed() // + '°C' // Convert from Kelvin to Celsius
  
  }
  else{
    alert(temperatureData.value)
    temperatureData.value = (Number(temperatureData.value) + 273.15).toFixed() // + '°K' // Convert from Kelvin to Celsius
  }
})

function locationSuccessCallback(position) {

  console.log('2 locationSuccessCallback')
  lat.value = position.coords.latitude;
  lon.value = position.coords.longitude
  console.log('3 lat value' + lat.value)
  fetch('https://api.openweathermap.org/data/2.5/weather?lat=' + lat.value +  '&lon=' + lon.value + '&appid=97c3dcd58e47ab9b00baac7d422371d3')
    .then(x => x.text())
    .then((data) => {
      data = JSON.parse(data)
      temperatureData.value = (data.main.temp - 273.15).toFixed() // + '°C' // Convert from Kelvin to Celsius
      descriptionData.value = data.weather[0].description
      cityData.value = data.sys.country + ', ' + data.name
    })

}


function locationShowError(error) {

  switch (error.code) {
    case error.PERMISSION_DENIED:
      alert("User denied the request for Geolocation.")
      break;
    case error.POSITION_UNAVAILABLE:
      alert("Location information is unavailable.")
      break;
    case error.TIMEOUT:
      alert("The request to get user location timed out.")
      break;
    case error.UNKNOWN_ERROR:
      alert("An unknown error occurred.")
      break;
  }
  
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="70" height="70" />
  </header>
  <main>
    <div class="container">
      <select v-model="temperatureUnit" name="" id="">
        <option value="kelvin">Kelvin</option>
        <option value="celsius">Celsius</option>
      </select>
    </div>
    <div class="container">
      <div class="column">
        <wdiget1 :temperature="temperatureData" :description="descriptionData" :city="cityData" />
      </div>
      <div class="column">
        <wdiget2 :temperature="temperatureData" :description="descriptionData" :city="cityData" />
      </div>
      <div class="column">
        <wdiget3 :temperature="temperatureData" :description="descriptionData" :city="cityData" />
      </div>
    </div>


  </main>
</template>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.column {
  padding: 50px;
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
