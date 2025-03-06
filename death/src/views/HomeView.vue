<template>
  <div>
    <h2>Data</h2>
    <div v-for="(item, index) in setData" :key="index">
      {{ item }}
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const setData = ref([]) // Should be an array, not a string

async function getData() {
  try {
    let res = await fetch(`https://data.cityofnewyork.us/resource/jb7j-dtam.json`)
    let data = await res.json()
    setData.value = data // Fix variable name
    console.log(data)
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

onMounted(() => {
  getData()
})
</script>

<style scoped></style>
