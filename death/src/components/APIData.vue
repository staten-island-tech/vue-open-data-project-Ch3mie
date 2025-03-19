<template>
  <div class="p-6 min-h-screen bg-gray-900">
    <h2 class="text-3xl font-bold text-white mb-6 text-center">Data</h2>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-6">
      <div
        v-for="(item, index) in setData"
        :key="index"
        class="bg-gray-800 border border-gray-700 shadow-lg rounded-xl p-6 hover:shadow-2xl transition-all text-white"
      >
        <h3 class="text-lg font-bold mb-2">Cause of Death: {{ item.leading_cause }}</h3>
        <p class="text-gray-300"><span class="font-semibold">Sex:</span> {{ item.sex }}</p>
        <p class="text-gray-300">
          <span class="font-semibold">Race:</span> {{ item.race_ethnicity }}
        </p>
        <p class="text-gray-300">
          <span class="font-semibold">Death Rate:</span> {{ item.death_rate }}
        </p>
        <p class="text-gray-300">
          <span class="font-semibold">Deaths:</span> {{ item.deaths }} deaths in {{ item.year }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, defineComponent, onMounted } from 'vue'

export default defineComponent({
  name: 'DataCards',
  setup() {
    const setData = ref([])

    const fetchData = async () => {
      try {
        const response = await fetch(
          'https://data.cityofnewyork.us/resource/jb7j-dtam.json?$limit=30',
        )
        const result = await response.json()
        setData.value = result
      } catch (error) {
        console.error('Failed to fetch data:', error)
      }
    }

    onMounted(() => {
      fetchData()
    })

    return { setData }
  },
})
</script>

<style scoped>
/* Add any additional scoped CSS here */
</style>
