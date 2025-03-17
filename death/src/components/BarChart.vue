<template>
  <Bar :data="chartData" :options="options" />
</template>

<script>
import { ref, defineComponent } from 'vue'
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
  name: 'BarChart',
  components: { Bar },
  setup() {
    const chartData = ref({
      labels: ['January', 'February', 'March'],
      datasets: [
        {
          label: 'Data One',
          backgroundColor: '#f87979',
          data: [40, 20, 12],
        },
      ],
    })

    const options = ref({})

    return { chartData, options }
  },
})
</script>
