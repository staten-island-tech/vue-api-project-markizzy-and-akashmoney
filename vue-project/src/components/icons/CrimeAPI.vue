<template>
    <div>

    </div>
</template>

<script>
import {ref, onMounted } from "vue";
const apiURL = ref("https://data.cityofnewyork.us/resource/uip8-fykc.json")
async function getData() {
  let res = await fetch(apiURL)
  let data = await res.json();
  apiURL.value = data.results;
}

onBeforeMounted(() => {
  getData();
})
</script>

<style lang="scss" scoped>

</style>