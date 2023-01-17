<script setup>
import wdiget1 from './components/wdiget1.vue'
import { onMounted } from 'vue';

onMounted(() => {
  fetch("https://api.openweathermap.org/data/2.5/weather?lat=38.0797&lon=46.3002&appid=97c3dcd58e47ab9b00baac7d422371d3")
    .then(x => x.text())
    .then(data => console.log(data))

})

</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
  </header>





  <main>

    <wdiget1 />

  </main>
</template>

<style scoped>
body {
  display: block;
}

header {
  line-height: 1.5;
  display: block;
  width: 100%;
}

main {
  margin: 70px;
}

.logo {
  display: block;
  margin: auto;
}
</style>
