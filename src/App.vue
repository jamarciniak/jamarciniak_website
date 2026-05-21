<script setup lang="ts">
// import { RouterLink } from 'vue-router'
import NavBar from './components/NavBar.vue'
import HomeView from './views/HomeView.vue'
</script>

<template>
  <div class="h-dvh overflow-hidden flex flex-col">
    <NavBar class="shrink-0" />
    <HomeView />
  </div>
</template>
