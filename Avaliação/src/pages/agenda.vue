<template>
   <v-container>
     <h2 class="text-h5 mb-4">Selecione uma ou mais salas</h2>
 
     <v-row v-for="letra in letras" :key="letra" class="mb-3">
       <v-col cols="12">
         <strong>Setor {{ letra }}</strong>
       </v-col>
 
       <v-col v-for="numero in 5" :key="`${letra}${numero}`" cols="auto">
         <v-btn
           :color="getCorSala(letra, numero)"
           :disabled="isAgendada(letra, numero)"
           @click="!isAgendada(letra, numero) && alternarSelecao(letra, numero)"
         >
           {{ letra }}{{ numero }}
         </v-btn>
       </v-col>
     </v-row>
 
     <v-row class="mt-6" justify="center" align="center">
       <v-btn color="success" class="mr-2" @click="agendarSalas" :disabled="selecionadas.size === 0">
         Agendar
       </v-btn>
       <v-btn color="error" @click="cancelarSelecao" :disabled="selecionadas.size === 0">
         Cancelar
       </v-btn>
     </v-row>
   </v-container>
 </template>
 
 <script setup>
 import { ref, onMounted } from 'vue'
 
 const letras = ['A', 'B', 'C', 'D', 'E']
 const selecionadas = ref(new Set())
 const agendadas = ref([])
 
 onMounted(() => {
   const data = JSON.parse(localStorage.getItem('salasAgendadas') || '[]')
   agendadas.value = data
 })
 
 function alternarSelecao(letra, numero) {
   const id = `${letra}${numero}`
   if (selecionadas.value.has(id)) {
     selecionadas.value.delete(id)
   } else {
     selecionadas.value.add(id)
   }
 }
 
 function isSelecionado(letra, numero) {
   return selecionadas.value.has(`${letra}${numero}`)
 }
 
 function isAgendada(letra, numero) {
   return agendadas.value.includes(`${letra}${numero}`)
 }
 
 function getCorSala(letra, numero) {
   const id = `${letra}${numero}`
   if (isAgendada(letra, numero)) return 'grey'
   if (selecionadas.value.has(id)) return 'green'
   return 'primary'
 }
 
 function agendarSalas() {
   const atuais = JSON.parse(localStorage.getItem('salasAgendadas') || '[]')
   const novas = Array.from(selecionadas.value)
   localStorage.setItem('salasAgendadas', JSON.stringify([...atuais, ...novas]))
   alert('Salas agendadas com sucesso!')
   selecionadas.value.clear()
   agendadas.value = [...atuais, ...novas]
 }
 
 function cancelarSelecao() {
   selecionadas.value.clear()
 }
 </script>
 