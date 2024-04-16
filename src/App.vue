<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <nav class="nav-bar">
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/profile">Profile</RouterLink>
    <RouterLink to="/login">Login</RouterLink> 
  </nav>

  <RouterView />  
</template>

<style scoped>
  .nav-bar {
    display: flex;
    width: 100%;
    height: 100px;
    background-color: #0f1463;
    font-size: 30px;
    justify-content: center;
    align-items: center;
  }

  .nav-bar a {
    color: white;
    text-decoration: none;
    margin: 0 60px;
    flex-direction: row;
    font-family: Snell Roundhand, cursive;
    
  }


 
</style>
