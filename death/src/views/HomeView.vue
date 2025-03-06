<template>
  <div>
    <h2>Data</h2>
    <div v-for="datas in data" :key=".id">
      {{ item }}
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
const route = useRoute()
const Data = ref('')
async function getData() {
  let res = await fetch(`https://data.cityofnewyork.us/resource/jb7j-dtam.json`)
  let data = await res.json()
  satData.value = data
  console.log(data)
  return data
}

onMounted(() => {
  getData()
})
</script>

<style scoped></style>
