<template>
  <div class="login">
    <h2>Login</h2>
    <form @submit.prevent="login">
      <label for="username">Username</label>
      <input type="text" id="username" v-model="form.username" required >
      <br>
      <label for="password">Password</label>
      <input type="password" id="password" v-model="form.password" required>
      <br>
    </form>
    <button type="submit">Login</button>
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

.login {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 50px;
  font-family: "Rubik", sans-serif;
  font-optical-sizing: auto;
  font-weight: weight;
  font-style: normal;
}

input[type="text"]{
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  margin-bottom: 10px; 
  margin-left: 12px;
}
input[type="password"] {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  margin-bottom: 10px; 
  margin-left: 15px;
}

button[type="submit"] {
  padding: 10px 20px;
  background-color: #0f1463;
  color: white;
  border: none;
  border-radius: 5px;
  font-size: 16px;
  cursor: pointer;
}


input[type="text"]:focus,
input[type="password"]:focus {
  outline: none;
  border-color: #0f1463; /* Change border color when focused */
}
</style>
