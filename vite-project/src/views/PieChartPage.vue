<template>
  <div class="pie-chart-container">
    <canvas ref="pieChartCanvas"></canvas>
  </div>
</template>


<script setup>


import { ref, onMounted } from 'vue';
import { Pie } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js';


const chartData = ref({});
const chartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  plugins: {
    title: {
      display: true,
      text: 'Number of Arrests per NYC Borough'
    }
  }
});


onMounted(async () => {
  try {


    const response = await fetch('https://data.cityofnewyork.us/resource/uip8-fykc.json');
    const data = await response.json();




    const boroughData = {};
    data.forEach(item => {
      const borough = item.arrest_boro;
      const pdCd = parseInt(item.pd_cd) || 0;
      if (!boroughData[borough]) {
        boroughData[borough] = 0;
      }
      boroughData[borough] += pdCd;
    });


    chartData.value = {
      labels: Object.keys(boroughData),
      datasets: [{
        label: 'Number of Arrests',
        backgroundColor: [
          'rgba(255, 99, 132, 0.6)',
          'rgba(54, 162, 235, 0.6)',
          'rgba(255, 206, 86, 0.6)',
          'rgba(75, 192, 192, 0.6)',
          'rgba(153, 102, 255, 0.6)',
          'rgba(255, 159, 64, 0.6)'
        ],
        borderWidth: 1,
        data: Object.values(boroughData)
      }]
    };
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>


<script>
export default {
  extends: Pie,
  mounted() {
    this.renderChart(chartData.value, chartOptions.value);
  }
};
</script>


<style>
.pie-chart-container {
  width: 100%;
  height: 400px;
}
</style>