<!-- <template>
    <div class="container mt-5">
        <h2 class="mb-4 text-center">Vue 3 Vuechart Js 5 Pie Chart Demo</h2>
        <Pie id="my-chart-id" :options="chartOptions" :data="chartData" />
    </div>
</template>
  
<script>
import { Pie } from 'vue-chartjs'
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from 'chart.js'
ChartJS.register(ArcElement, Tooltip, Legend)

export default {
    name: 'PieChart',
    components: { Pie },
    data() {
        return {
            chartData: {
                labels: ['VueJs', 'EmberJs', 'ReactJs', 'AngularJs'],
                datasets: [
                    {
                        backgroundColor: ['#41B883', '#E46651', '#00D8FF', '#DD1B16'],
                        data: [40, 20, 80, 10]
                    }
                ]
            },
            chartOptions: {
                responsive: true
            }
        }
    }
}
</script> -->