<template>
  <Bar
    id="my-chart-id"
    :options="chartOptions"
    :data="chartData"
  />
</template>

<script>
import { Bar } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: { Bar },
  data() {
    return {
      chartData: {
        labels: [ 'January', 'February', 'March' ],
        datasets: [ { data: [40, 20, 12] } ]
      },
      chartOptions: {
        responsive: true
      }
    }
  }
}
</script>
  <script setup>
  const api= "https://data.cityofnewyork.us/resource/uip8-fykc.json"
import { ref, onMounted  } from 'vue';
let apiURL = ref('');
async function getData() {
  let res = await fetch(api)
  let data = await res.json();
  console.log(data)
  apiURL.value = data;
};
 onMounted (() => {
  getData();

})</script>