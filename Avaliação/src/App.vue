<template>
  <v-app id="inspire">
    <!-- Menu lateral, só aparece após login -->
    <v-navigation-drawer v-model="drawer" v-if="isAuthenticated">
      <Menu @authenticated="login" />
    </v-navigation-drawer>

    <!-- Barra superior -->
    <v-app-bar v-if="isAuthenticated">
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <v-app-bar-title>Controle de Reservas</v-app-bar-title>
    </v-app-bar>

    <!-- Conteúdo principal -->
    <v-main>
      <v-container>
        <!-- Login -->
        <Login v-if="!isAuthenticated" color="red" @authenticated="login" />

        <!-- Roteamento automático -->
        <router-view v-else />
      </v-container>
    </v-main>
  </v-app>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import Menu from '@/components/Menu.vue'
import Login from './components/Login.vue'

const drawer = ref(null)
const isAuthenticated = ref(false)
const router = useRouter()

const login = (value) => {
  isAuthenticated.value = value
  document.cookie = `isAuthenticated=${value}`

  if (value) {
    router.push('/') // redireciona após login
  } else {
    router.push('/login') // redireciona após logout (adicione uma rota se necessário)
  }
}

onMounted(() => {
  const result = document.cookie.split(';').find(e => e.trim().startsWith('isAuthenticated'))
  if (result) {
    isAuthenticated.value = result.split('=')[1] === 'true'
  }
})
</script>
