<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const users = ref([])
const loginError = ref(false)
const logged = ref(false)

const getUsers = async () => {
    const response = await fetch('src/users.json')
    users.value = await response.json()
}

getUsers()

const handleSubmit = () => {
  const usersMap = new Map(users.value.map(user => [user.email, user]));
  const user = usersMap.get(email.value);

  if (user && user.password === password.value) {
    logged.value = true
    loginError.value = false
  } else {
    loginError.value = true
    logged.value = false
  }
}
</script>

<template>
  <div>
    <h1>Inicio de sesión</h1>
    <form action="POST">
      <label for="email">Email:</label>
      <input type="email" v-model="email" />

      <label for="password">Password:</label>
      <input type="password" v-model="password" />

      <button @click="handleSubmit" type="button">Ingresar</button>
    </form>
    <p v-if="loginError" class="error">El usuario no existe</p>
    <p v-if="logged" class="success">Inicio de sesión exitoso</p>
  </div>
</template>

