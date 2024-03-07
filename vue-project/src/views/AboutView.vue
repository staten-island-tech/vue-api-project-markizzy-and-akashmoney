<template>
  <div>

  </div>
</template>

<script setup>
import {ref, onMounted } from "vue";
const apiURL = ref("")
async function getSOMETHING() {
  let res = await fetch //(link)
  let data = await res.json();
  apiURL.value = data.results;
}

onBeforeMounted(() => {
  getSOMETHING();
})
</script>

<style scoped>

</style>