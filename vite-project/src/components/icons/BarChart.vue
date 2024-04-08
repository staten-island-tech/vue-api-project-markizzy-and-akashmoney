<template>
  <div class="chart-container">
    <Bar
      id="my-chart-id"
      :options="chartOptions"
      :data="chartData"
      :style="{width: '1000px', height: '1000px'}" 
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Bar } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale);

const apiUrl = "https://data.cityofnewyork.us/resource/uip8-fykc.json";
const chartData = ref({
  labels: [],
  datasets: [{
    label: 'Arrests',
    borderWidth: 1,
    data: []
  }]
});
const chartOptions = ref({
  responsive: true
});

onMounted(async () => {
  try {
    const res = await fetch(apiUrl);
    const data = await res.json();
    console.log(data);
    const newData = {
      labels: data.map(item => item.ofns_desc), // Assuming there's an 'arrest_date' property in each item
      datasets: [{
        label: 'Number of Arrests Per Year',
        data: data.map(item => item.pd_cd) // Assuming there's an 'arrest_count' property in each item
      }]
    };
    chartData.value = newData;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>

