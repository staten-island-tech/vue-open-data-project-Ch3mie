<template>
  <div>
    <h2>Data</h2>
    <div v-for="(item, index) in setData" :key="index">
      <p>Race: {{ item.race_ethnicity }}</p>
      <p>Sex: {{ item.sex }}</p>
      <p>Cause of Death:{{ item.leading_cause }}</p>
      <p>Death Rate: {{ item.death_rate }}</p>
      <p>Deaths: {{ item.deaths }} deaths in {{ item.year }}</p>
      <p>____________________________</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const setData = ref([])

async function getData() {
  try {
    let res = await fetch(`https://data.cityofnewyork.us/resource/jb7j-dtam.json`)
    let data = await res.json()
    setData.value = data
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
