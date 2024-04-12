<template>
  <div>
    <div class="band"></div>
    <div>
      <img :src="user.profilePicture" alt="Profile Picture" />
      <span>{{ user.username }}</span>
      <ul>
        <li v-for="game in user.games" :key="game.id">
          {{ game.title }} - Scored: {{ game.grade }} - Status: {{ game.status }}
        </li>
      </ul>
    </div>
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


.band {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  background-color: rgb(22, 22, 47);
  height: 300px; 
}

img {
  position: absolute;
  top: 150px; 
  left: 15%; 
  width: 150px;
  height: 150px;
}

span {
  position: absolute;
  top:260px;
  left: 27%; 
  font-size: 24px;
  font-family: Snell Roundhand, cursive;
  color: white; 
}

li {
  background-color: gray;
  padding: 18px;
  margin-bottom: 20px;
  text-align: left;
  font-size: 16px;
  font-family: Arial;
  width: 50%;
  margin-left: 40%; 
  margin-right: auto;
}
ul {
  display: flex;
  flex-direction: column;
  align-items: center;
  list-style-type: none;
  padding: 0;
  margin-top: 350px;
}
</style>