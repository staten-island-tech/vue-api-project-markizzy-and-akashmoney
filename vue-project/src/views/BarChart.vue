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
import{ref , onMounted, onBeforeMount} from 'vue';
const apiUrel=ref("https://data.cityofnewyork.us/api/odata/v4/uip8-fykc")
async function getData(){
  let res= await fetch(apiUrel);
  let data = await res.json()
  apiUrel.value= data.results
}

onBeforeMounted(()=>{
  getData();
})

</script>