<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <nav class="bg-gray-800 text-white p-4 shadow-lg">
    <div class="container mx-auto flex justify-center space-x-6">
      <RouterLink to="/" class="px-4 py-2 rounded-lg hover:bg-gray-700 transition duration-300">
        Home
      </RouterLink>
      <RouterLink
        to="/about"
        class="px-4 py-2 rounded-lg hover:bg-gray-700 transition duration-300"
      >
        Bar Chart
      </RouterLink>
      <RouterLink to="/pie" class="px-4 py-2 rounded-lg hover:bg-gray-700 transition duration-300">
        Pie Chart
      </RouterLink>
    </div>
  </nav>
  <div class="p-6">
    <RouterView />
  </div>
</template>

<style scoped>
nav a.router-link-exact-active {
  background-color: #4a5568; /* Darker gray for active links */
  font-weight: bold;
}
</style>
