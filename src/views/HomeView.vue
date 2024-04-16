<script setup>
import { ref, computed } from 'vue'

const games = ref([])
const search = ref('');
const searchQuery = ref('')

fetch('/src/data/games.json')
  .then(response => response.json())
  .then(data => {
    games.value = data
  })

function navigateToGamePage(gameId) {
  router.push(`/views/game_pages/${gameId}`);
}


const sortedGames = computed(() => {
  return this.games.sort((a, b) => a.name.localeCompare(b.name));
})



const bestGames = computed(() => {
  return games.value.sort((a, b) => b.average_rating - a.average_rating).slice(0, 5)
})

const worstGames = computed(() => {
  return games.value.sort((a, b) => a.average_rating - b.average_rating).slice(0, 5)
})

const latestGames = computed(() => {
  return games.value.sort((a, b) => new Date(b.release_date) - new Date(a.release_date)).slice(0, 5)
})

const sortedGameNames = computed(() => {
  return games.value.sort((a, b) => a.name.localeCompare(b.name)).map(game => game.name);
});

</script>

<template>
  <div class="game-collection">
    <h1>GameList</h1>
      <input 
        type="text" 
        id="game-search" 
        list="games" 
        v-model="searchQuery" 
        placeholder="Search for a game . . ."
        @keyup.enter="navigateToGamePage(selectedGame.id)">
      <datalist id="games">
        <option v-for="game in sortedGameNames" :key="game" :value="game"></option>
      </datalist>
      <div class="game-lists">
      <div class="game-list">
        <h2>Best Rated Games</h2>
        <ul>
          <li v-for="game in bestGames" :key="game.id">
            <h3>{{ game.name }}</h3>
            <p>Average rating: {{ game.average_rating }}</p>
            <p>Release date: {{ game.release_date }}</p>
          </li>
        </ul>
      </div>
      <div class="game-list">
        <h2>Worst Rated Games</h2>
        <ul>
          <li v-for="game in worstGames" :key="game.id">
            <h3>{{ game.name }}</h3>
            <p>Average rating: {{ game.average_rating }}</p>
            <p>Release date: {{ game.release_date }}</p>
          </li>
        </ul>
      </div>
      <div class="game-list">
        <h2>Latest Added Games</h2>
        <ul>
          <li v-for="game in latestGames" :key="game.id">
            <h3>{{ game.name }}</h3>
            <p>Average rating: {{ game.average_rating }}</p>
            <p>Release date: {{ game.release_date }}</p>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.game-collection {
  max-width: 800px;
  margin: 0 auto;
}

.game-lists {
  display: flex;
  justify-content: space-between;
}

.game-list {
  flex: 1;
}

ul {
  list-style: none;
  padding: 0;
}

input[type='text'] {
  width: 100%;
  padding: 0.5em;
  font-size: 1em;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-sizing: border-box;
  margin-bottom: 1em;
}

input[type='text']:focus {
  outline: none;
  border-color: #666;
}
</style>
