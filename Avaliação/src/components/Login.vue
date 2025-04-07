<template>
  <div id="login-container">
    <div id="login">
      <h1 :style="'color:' + props.color">LOGIN</h1>

      <input
        type="text"
        placeholder="Usuário"
        v-model="user"
        :style="{ color: 'black', backgroundColor: 'white' }"
      />
      <input
        type="password"
        placeholder="Senha"
        v-model="pass"
        :style="{ color: 'black', backgroundColor: 'white' }"
      />

      <button @click="login">Entrar</button>
    </div>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'
import { useRouter } from 'vue-router'

const emits = defineEmits(['authenticated'])
const props = defineProps({ color: String })
const router = useRouter()

const user = ref('')
const pass = ref('')

const login = () => {
  if (user.value === 'teste' && pass.value === '123') {
    emits('authenticated', true)
    router.push('/')
  }
}
</script>

<style>
#login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #131212;
}

#login {
  background-color: white;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 400px;
  text-align: center;
}

#login h1 {
  margin-bottom: 30px;
  font-size: 28px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 12px;
  margin-bottom: 20px;
  border: 2px solid #ccc;
  border-radius: 8px;
  outline: none;
  transition: border-color 0.3s;
}

input:focus {
  border-color: #1976d2;
}

button {
  width: 100%;
  padding: 12px;
  background-color: #1976d2;
  color: white;
  border: 2px solid #1976d2;
  border-radius: 8px;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s, border-color 0.3s;
}

button:hover {
  background-color: #1565c0;
  border-color: #1565c0;
}
</style>
