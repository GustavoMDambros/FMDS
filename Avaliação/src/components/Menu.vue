<script setup>
import { ref, defineEmits } from 'vue'

const emit = defineEmits(['authenticated'])

const items = ref([
  { title: 'Início', icon: 'mdi-home', link: '/' },
  { title: 'Agenda', icon: 'mdi-account', link: '/agenda' },
  { title: 'Reservas', icon: 'mdi-file', link: '/reservas' },
  { title: 'Sair', icon: 'mdi-logout', action: 'logout' },

])

const handleItemClick = (item) => {
  if (item.action === 'logout') {
    emit('authenticated', false) // aqui está o logout
  }
}
</script>

<template>
  <v-list>
    <v-list-item
      prepend-avatar="https://cdn-icons-png.flaticon.com/512/147/147142.png"
      subtitle="teste@email.com"
      title="Teste"
    />
  </v-list>

  <v-divider />

  <v-list>
    <v-list-item
      v-for="item in items"
      :key="item.title"
      link
      :prepend-icon="item.icon"
      :title="item.title"
      :to="item.link"
      @click="handleItemClick(item)"
    />
  </v-list>
</template>
