<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/profile">Profile</RouterLink>
    <RouterLink to="/login">Login</RouterLink> 
  </nav>

  <RouterView />  
</template>

<style scoped>
</style>
