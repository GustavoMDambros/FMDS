<template>
    <v-container>
      <h2 class="text-h5 mb-4">Minhas reservas</h2>
  
      <v-row v-for="letra in letras" :key="letra" class="mb-3">
        <v-col cols="12">
          <strong>Setor {{ letra }}</strong>
        </v-col>
  
        <v-col v-for="numero in 5" :key="`${letra}${numero}`" cols="auto">
          <v-btn
            :color="isAgendada(letra, numero) ? 'green' : 'grey-lighten-2'"
            :disabled="!isAgendada(letra, numero)"
          >
            {{ letra }}{{ numero }}
          </v-btn>
        </v-col>
      </v-row>
  
      <v-row class="mt-6" justify="center">
        <v-btn color="error" @click="limparAgendamentos">
          Limpar Agendamentos
        </v-btn>
      </v-row>
    </v-container>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  
  const letras = ['A', 'B', 'C', 'D', 'E']
  const agendadas = ref([])
  
  onMounted(() => {
    const stored = JSON.parse(localStorage.getItem('salasAgendadas') || '[]')
    agendadas.value = stored
  })
  
  function isAgendada(letra, numero) {
    return agendadas.value.includes(`${letra}${numero}`)
  }
  
  function limparAgendamentos() {
    if (confirm('Deseja realmente limpar todos os agendamentos?')) {
      localStorage.removeItem('salasAgendadas')
      agendadas.value = []
    }
  }
  </script>
  