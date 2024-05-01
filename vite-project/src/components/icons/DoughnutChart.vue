<template>
  <div class="chart-container">
    <Doughnut
      id="my-chart-id"
      :options="chartOptions"
      :data="chartData"
      :style="{ width: '1000px', height: '400px' }"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Doughnut } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, DoughnutController, ArcElement } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, DoughnutController, ArcElement);

const apiUrl = "https://data.cityofnewyork.us/resource/uip8-fykc.json";
const chartData = ref({
labels: [
'Staten Island',
'Brooklyn',
'Manhattan',
'Bronx',
'Queens',
],
datasets: [{
  label: 'Number of Arrests',
  backgroundColor: [
    'rgb(255, 99, 132)',  
    'rgb(54, 162, 235)',  
    'rgb(255, 159, 64)',  
    'rgb(75, 192, 192)',  
    'rgb(153, 102, 255)'  
  ],
  borderColor: 'white',
  borderWidth: 1,
  data: []
}]
});



onMounted(async () => {
try {
  const res = await fetch(apiUrl);
  const data = await res.json();

  const arrestsByBorough = {};
  data.forEach(item => {
    const borough = item.arrest_boro;
    const pd_cd = item.pd_cd;
    if (!arrestsByBorough[borough]) {
      arrestsByBorough[borough] = 0;
    }
    arrestsByBorough[borough] += parseInt(pd_cd); // Increment arrest count by pd_cd
  });


  const boroughLabels = Object.keys(arrestsByBorough);
  const arrestCounts = Object.values(arrestsByBorough);
 
  const backgroundColors = generateBackgroundColors(boroughLabels.length);
 


 this.chartData.value.labels = boroughLabels;
  this.chartData.value.datasets[0].data = arrestCounts;
  this.chartData.value.datasets[0].backgroundColor = backgroundColors;
} catch (error) {
  console.error('Error fetching data:', error);
}
});


function generateBackgroundColors(count) {
const colors = [];
for (let i = 0; i < count; i++) {
  const color = `rgba(${Math.floor(Math.random() * 256)}, ${Math.floor(Math.random() * 256)}, ${Math.floor(Math.random() * 256)}, 0.6)`;
  colors.push(color);
}
return colors;
}


</script>




