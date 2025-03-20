<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-900 p-6">
    <div class="w-full max-w-2xl bg-gray-800/90 border-2 border-black shadow-lg rounded-xl p-6">
      <h2 class="text-2xl font-bold text-white text-center mb-4">Deaths by Leading Cause</h2>
      <div v-if="loading" class="text-center text-gray-300">Loading...</div>
      <Pie v-else :data="chartData" :options="options" class="h-[400px]" />
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Pie } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale } from 'chart.js'

// Register necessary chart components
ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale)

// Reactive state
const chartData = ref({
  labels: [],
  datasets: [],
})
const loading = ref(true)

// Chart options
const options = {
  responsive: true,
  plugins: {
    legend: {
      position: 'top',
    },
    title: {
      display: true,
      text: 'Deaths by Leading Cause',
    },
  },
}

// Fetch and process data
const fetchData = async () => {
  try {
    const response = await fetch('https://data.cityofnewyork.us/resource/jb7j-dtam.json?$limit=30')
    const result = await response.json()

    const labels = result.map((item) => item.leading_cause)
    const data = result.map((item) => parseInt(item.deaths, 10))

    chartData.value = {
      labels,
      datasets: [
        {
          label: 'Deaths',
          backgroundColor: ['#FF6384', '#36A2EB', '#FFCE56', '#4BC0C0', '#9966FF', '#FF9F40'],
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

// Load data on mount
onMounted(fetchData)
</script>
