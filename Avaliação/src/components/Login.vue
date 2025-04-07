<template>
  <div id="login">
    <h1 :style="'color:' + props.color">Autenticação</h1>
    <input type="text" placeholder="Usuário" v-model="user" />
    <input type="password" placeholder="Senha" v-model="pass" />
    <button @click="login">Entrar</button>

    <ul>

    </ul>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits, watch, watchEffect } from 'vue'
import { useRouter } from 'vue-router' // 🚨 IMPORTANTE para navegação

const emits = defineEmits(['authenticated'])
const props = defineProps({ color: String })
const router = useRouter() // 🚀 Instância do roteador

const user = ref('')
const pass = ref('')
const check = ref({
  size: false,
  lowercase: false,
  uppercase: false,
  number: false,
  special: false
})

const login = () => {
  if (user.value === 'teste' && pass.value === '123') {
    emits('authenticated', true)
    router.push('/') // 👉 Redireciona para a página index.vue
  }
}

watch(pass, (value) => {
  check.value.size = value.length > 6
  check.value.lowercase = /[a-z]/.test(value)
  check.value.uppercase = /[A-Z]/.test(value)
  check.value.number = /[0-9]/.test(value)
  check.value.special = /[^a-zA-Z0-9]/.test(value)
})

watchEffect(() => {
  console.log('Senha:', pass.value)
  console.log('Usuário:', user.value)
  console.log('Tamanho:', check.value.size)
})
</script>

<style>
#login {
  max-width: 700px;
  margin: auto;
}

input {
  width: 100%;
  padding: 10px;
  margin: 10px 0;
}
</style>
