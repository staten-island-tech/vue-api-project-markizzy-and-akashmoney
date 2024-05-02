<template>
  <div class="chart-container">
    <Doughnut :options="chartOptions" :data="chartData" />
  </div>
</template>

<script>
import { Doughnut } from 'vue-chartjs';

export default {
  components: {
    Doughnut
  },
  data() {
    return {
      chartData: {
        labels: ['Red', 'Blue', 'Yellow'],
        datasets: [{
          label: 'My Doughnut Chart',
          data: [300, 50, 100],
          backgroundColor: [
            'rgb(255, 99, 132)',
            'rgb(54, 162, 235)',
            'rgb(255, 205, 86)'
          ]
        }]
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      }
    };
  }
};
</script>

<style scoped>
.chart-container {
  width: 400px;
  height: 400px;
  margin: auto;
}
</style>


