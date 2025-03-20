<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-900 p-6">
    <div class="w-full max-w-4xl bg-gray-800/90 border-2 border-black shadow-lg rounded-xl p-6">
      <h2 class="text-2xl font-bold text-white text-center mb-4">Death Statistics Chart</h2>
      <div class="w-full h-[500px]">
        <Bar :data="chartData" :options="options" />
      </div>
      <p v-if="loading" class="text-center text-gray-300 mt-4">Loading...</p>
    </div>
  </div>
</template>

<script>
import { ref, defineComponent, onMounted } from 'vue'
import { Bar } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default defineComponent({
  name: 'ChartWithAPI',
  components: { Bar },
  setup() {
    const chartData = ref({
      labels: [],
      datasets: [],
    })
    const options = ref({
      responsive: true,
      maintainAspectRatio: false, // Allows the chart to fill the container
    })
    const loading = ref(true)

    const fetchData = async () => {
      try {
        const response = await fetch(
          'https://data.cityofnewyork.us/resource/jb7j-dtam.json?$limit=30',
        )
        const result = await response.json()

        const labels = result.map((item) => item.leading_cause)
        const data = result.map((item) => parseInt(item.deaths, 10))

        chartData.value = {
          labels,
          datasets: [
            {
              label: 'Deaths',
              backgroundColor: '#f87979',
              data,
            },
          ],
        }
        loading.value = false
      } catch (error) {
        console.error('Failed to fetch data:', error)
        loading.value = false
      }
    }

    onMounted(() => {
      fetchData()
    })

    return { chartData, options, loading }
  },
})
</script>
