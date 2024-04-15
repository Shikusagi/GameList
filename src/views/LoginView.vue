<template>
  <div>
    <h2>Login</h2>
    <form @submit.prevent="login">
      <label for="username">Username:</label>
      <input type="text" id="username" v-model="form.username" required>
      <br>
      <label for="password">Password:</label>
      <input type="password" id="password" v-model="form.password" required>
      <br>
      <button type="submit">Login</button>
    </form>
    <p v-if="error" style="color: red;">{{ error }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import users from '../data/users.json' 
import { useRouter } from 'vue-router'

const form = ref({
  username: '',
  password: ''
})

const error = ref('')
const router = useRouter();

const login = () => {
  const { username, password } = form.value
  const user = users.find(u => u.username === username && u.password === password)
  if (user) {
    console.log('Logged in successfully!', user)
    router.push('/')
  } else {
    error.value = 'Invalid username or password.'
  }
}
</script>


<style scoped>

</style>
