<template>
  <v-container>
    <h2 class="text-h5 mb-4">Salas Disponíveis</h2>

    <v-row v-for="letra in letras" :key="letra" class="mb-3">
      <v-col cols="12">
        <strong>Setor {{ letra }}</strong>
      </v-col>

      <v-col v-for="numero in 5" :key="`${letra}${numero}`" cols="auto">
        <v-btn
          :color="getCorSala(letra, numero)"
          :disabled="true"
        >
          {{ letra }}{{ numero }}
        </v-btn>
      </v-col>
    </v-row>

    <v-row class="mt-6" justify="center" align="center">
      <v-btn color="primary" @click="irParaAgenda">
        Ir para o agendamento
      </v-btn>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const letras = ['A', 'B', 'C', 'D', 'E']
const agendadas = ref([])
const router = useRouter()

onMounted(() => {
  const data = JSON.parse(localStorage.getItem('salasAgendadas') || '[]')
  agendadas.value = data
})

function isAgendada(letra, numero) {
  return agendadas.value.includes(`${letra}${numero}`)
}

function getCorSala(letra, numero) {
  const id = `${letra}${numero}`
  return isAgendada(letra, numero) ? 'red' : 'primary'
}

function irParaAgenda() {
  router.push('/agenda')
}
</script>
