<script setup>
import { ref } from 'vue'

const email = ref('')
const password = ref('')
const users = ref([])
const loginError = ref(false)
const logged = ref(false)
const emailStorage = ref('')

const getUsers = async () => {
  const response = await fetch('src/users.json')
  users.value = await response.json()
}

const checkLocalStorage = () => {
  const isLogged = localStorage.getItem('isLogged') === 'true'  
  logged.value = isLogged
  if (isLogged) {
    emailStorage.value = localStorage.getItem('emailLogged')
  }
}

getUsers()
checkLocalStorage()

const handleSubmit = () => {
  const usersMap = new Map(users.value.map(user => [user.email, user]));
  const user = usersMap.get(email.value);

  if (user && user.password === password.value) {
    logged.value = true
    loginError.value = false
    localStorage.setItem('isLogged', 'true')
    localStorage.setItem('emailLogged', user.email)
    window.location.reload()
  } else {
    loginError.value = true
    logged.value = false
  }
}

const logout = () => {
  logged.value = false
  localStorage.removeItem('isLogged')
  localStorage.removeItem('emailLogged')
  window.location.reload()
}
</script>

<template>
  <div>
    <h1 v-if="!logged">Inicio de sesión</h1>
    <form action="POST" v-if="!logged">
      <label for="email">Email:</label>
      <input type="email" v-model="email" />

      <label for="password">Password:</label>
      <input type="password" v-model="password" />

      <button @click="handleSubmit" type="button">Ingresar</button>
    </form>
    <p v-if="loginError" class="error">El usuario no existe</p>
    <p v-if="logged" class="success">Inicio de sesión exitoso</p>
    <p v-if="logged" class="account">{{ emailStorage }}</p>

    <h2 v-if="logged">Tabla de usuarios</h2>
    <table v-if="logged">
      <thead>
        <tr>
          <th>ID</th>
          <th>Username</th>
          <th>Email</th>
          <th>Age</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="u in users">
          <td>{{ u.id }}</td>
          <td>{{ u.username }}</td>
          <td>{{ u.email }}</td>
          <td>{{ u.age }}</td>
        </tr>
      </tbody>
    </table>

    <button @click="logout" v-if="logged">Cerrar sesión</button>


  </div>
</template>
