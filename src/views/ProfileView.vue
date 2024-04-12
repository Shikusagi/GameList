<template>
  <div v-if="user">
    <div>
      <div>
        <div class="user-info">
          <img class="user-pic" :src="user.profilePicture" alt="Profile Picture" />
          <span class="user-name">{{ user.username }}</span>
        </div>
        
        <ul>
          <li v-for="game in user.games" :key="game.id">
            <div class="game-item">
              <img :src="game.pic" alt="Game Picture" class="game-picture" />
              <span>{{ game.status }} {{ game.title }} - Scored: {{ game.grade }}</span>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
  <div v-else>
    <p>You are not logged in...</p>
   
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import users from '../data/users.json';

const user = ref({
  username: '',
  profilePicture: '',
  games: []
});

// Load data from JSON file
onMounted(async () => {
  try {
    user.value = users[0];
  } catch (error) {
    console.error('Error loading data:', error);
  }
});
</script>

<style scoped>

.user-info{
  display: flex;
  flex-direction: row;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  background-color: rgb(22, 22, 47);
  height: 300px; 
  gap: 10px;
}

.user-pic {
  width: 150px;
  height: 150px;
  margin-left: 20%;
  margin-top: 150px;
}

.user-name {
  font-size: 24px;
  font-family: Snell Roundhand, cursive;
  color: white;
  margin-top: 260px;
  margin-left: 15px;
}

li {
  background-color: rgb(176, 191, 235);
  padding: 18px;
  margin-bottom: 20px;
  text-align: left;
  font-size: 16px;
  font-family: Arial;
  width: 50%;
  height: 60px;
  margin-left: 45%; 
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

.game-picture {
  width: 70px;
  height: 70px;
  margin-top: -0.5%;
}

.game-item {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 10px;
}

</style>