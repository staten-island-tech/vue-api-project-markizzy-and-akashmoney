<template>
  <div class="chart-container">
    <Bar
      id="my-chart-id"
      :options="chartOptions"
      :data="chartData"
      :style="{width: '1000px', height: '400px'}" 
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
    label: 'Number of Arrests',
    backgroundColor: 'rgba(153, 102, 255, 0.6)', 
    borderColor: 'rgba(153, 102, 255, 1)', 
    borderWidth: 1,
    data: []
  }]
});
const chartOptions = ref({
  responsive: true,
  maintainAspectRatio: false,
  scales: {
    y: {
      beginAtZero: true
    }
  },
  plugins: {
    title: {
      display: true,
      text: 'NYC Yearly Arrest Data '
    }
  }
});

onMounted(async () => {
  try {
    const res = await fetch(apiUrl);
    const data = await res.json();
    
  
    const groupedData = {};
    data.forEach(item => {
      const offense = item.ofns_desc;
      if (!groupedData[offense]) {
        groupedData[offense] = 0;
      }
      groupedData[offense] += parseInt(item.pd_cd); // I HAVE NO IDEA WHAT THIS DOES
    });

   
    const sortedData = Object.entries(groupedData)
      .sort((a, b) => b[1] - a[1]);

   
    const labels = sortedData.slice(0, 10).map(entry => entry[0]);
    const arrestCounts = sortedData.slice(0, 10).map(entry => entry[1]);

    const newData = {
      labels: labels,
      datasets: [{
        label: 'Number of Arrests',
        backgroundColor: 'rgba(153, 102, 255, 0.6)', 
    borderColor: 'rgba(153, 102, 255, 1)', 
        borderWidth: 1,
        data: arrestCounts
      }]
    };

    chartData.value = newData;
  } catch (error) {
    console.error('Error fetching data:', error);
    
  }
});
</script>