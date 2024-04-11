<template>
  <div>
    <img :src="user.profilePicture" alt="Profile Picture" />
    <span>{{ user.username }}</span>
    <ul>
      <li v-for="game in user.games" :key="game.id">
        {{ game.title }} - {{ game.grade }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const user = ref({
  username: '',
  profilePicture: '',
  games: []
});

// Load data from JSON file
onMounted(async () => {
  try {
    const response = await fetch('../user_data.json');
    const data = await response.json();
    user.value = data.user;
  } catch (error) {
    console.error('Error loading data:', error);
  }
});
</script>

<style scoped>
img {
  width: 100px;
  height: 100px;
}
</style>
