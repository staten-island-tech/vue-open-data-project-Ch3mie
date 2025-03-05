<template>
  <div>
    <h2>Data</h2>
    <div v-for="(item, index) in SetData" :key="index">
      {{ item.brth_yr }}
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const SetData = ref([])

async function getData() {
  try {
    let res = await fetch(`https://data.cityofnewyork.us/resource/25th-nujf.json`)
    let data = await res.json()
    SetData.value = data
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
