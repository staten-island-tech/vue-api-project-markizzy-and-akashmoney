<template>
  <div class="container">
    <Bar id="my-chart-id"
 :options="chartOptions"
 v-if="loaded" 
 :data="chartData" /> />
  </div>
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
  data: () => ({
    loaded: false,
    chartData: null
  }),
  async mounted () {
    this.loaded = false

    try {
      const { userlist } = await fetch('/api/userlist')
      this.chartdata = userlist

      this.loaded = true
    } catch (e) {
      console.error(e)
    }
  }
}
</script>
 
<script setup>

const api = "https://data.cityofnewyork.us/resource/uip8-fykc.json";

import {ref , onMounted } from 'vue';
let apiUrl = ref('')
async function getData (){
  let res = await fetch(api)
  let data = await res.json();
  console.log(data)
  apiUrl.value = data;
};
const data = onMounted (()=> {
  getData();
})</script>