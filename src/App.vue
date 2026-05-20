<script setup lang="ts">
// import { RouterLink } from 'vue-router'
import NavBar from './components/NavBar.vue'
import HomeView from './views/HomeView.vue'
</script>

<template>
  <header>
    <NavBar />
    <HomeView />
    <!-- <nav>
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">About</RouterLink>
    </nav> -->
  </header>
</template>
