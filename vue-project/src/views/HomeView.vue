<template>

  <div>



  </div>

</template>



<script>

// https://data.cityofnewyork.us/resource/uip8-fykc.json
import { ref, onMounted } from 'vue';
let apiURL = ref('');
async function getData() {
  let res = await fetch("https://data.cityofnewyork.us/resource/s67q-ee5u.json")
  let data = await res.json();
  console.log(data)
  apiURL.value = data;
}

onMounted (() => {
  getData();
})



</script>

<style scoped>

</style>