<script setup>
import { ref } from 'vue';

const username = 'Shiku';
const entries = ref([
  { id: 1, title: 'Fortnite' },
  { id: 2, title: 'Dofus' },
  { id: 3, title: 'Genshin Impact' },
]);


</script>

<template>
  <div>
    <img src="https://i.imgur.com/FfqCvuB.jpeg" alt="Profile Picture" />
    <span>{{ username }}</span>
    <ul>
      <li v-for="entry in entries" :key="entry.id">{{ entry.title }}</li>
    </ul>
  </div>
</template>


<style scoped>
img {
  width: 100px;
  height: 100px;
}
</style>