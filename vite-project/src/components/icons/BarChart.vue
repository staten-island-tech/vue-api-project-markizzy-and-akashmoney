<template>
  <Bar
    id="my-chart-id"
    :options="chartOptions"
    :data="chartData"
    class="chart-container" 
  />
</template>

<script>
import { Bar } from 'vue-chartjs'

export default {
  name: 'BarChart',
  components: { Bar },
  data() {
    return {
      chartData: {
        labels: ['January', 'February', 'March'],
        datasets: [{ data: [40, 20, 12] }]
      },
      chartOptions: {
        responsive: true
      }
    }
  }
}
</script>

<style src="./styles.css"></style> <!-- Import external stylesheet -->



