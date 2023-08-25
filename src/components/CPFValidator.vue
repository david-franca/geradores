<script setup lang="ts">

import {ref} from "vue";

const isValid = ref<boolean>()
const cpfForm = ref<string>('')

function isSequence(cpf: string): boolean {
  return cpf[0].repeat(11) === cpf
}

function generateDigit(cpf: string): string {
  const cpfArray: number[] = cpf.split('').map(n => parseInt(n))
  let regressive: number = cpfArray.length + 1
  const total: number = cpfArray.reduce((acc, val) => {
    acc += (val * regressive--)
    return acc
  }, 0)
  const digit: number = 11 - (total % 11)
  return digit > 9 ? '0' : String(digit)
}

function clean(value: string): string {
  return value.replace(/\D/g, '')
}

function generateNewCpf(value: string): string {
  const cpf: string = value.slice(0, -2)
  const digit1: string = generateDigit(cpf)
  const digit2: string = generateDigit(cpf + digit1)
  return cpf + digit1 + digit2
}

function validate(value: string) {
  const cpf = clean(value)
  if (cpf.length !== 11) return false
  if (isSequence(cpf)) return false
  const newCpf: string = generateNewCpf(cpf)
  isValid.value = newCpf === cpf
}

function onValidate() {
  validate(cpfForm.value)
}
</script>

<template>
  <v-sheet elevation="12"
           height="90vh"
           rounded="lg"
           width="100%"
           class="pa-4 text-center mx-auto bg-teal-darken-3 justify-center align-center d-flex flex-column ">
    <h1 class="title">Validador de CPF</h1>
    <h4 class="subtitle">Digite um CPF e clique em <strong>"Validar CPF"</strong> para verificar se ele é válido ou
      falso</h4>
    <input class="resultado" v-model="cpfForm"/>
    <v-btn color="primary" class="mt-2" @click="onValidate">Validar CPF</v-btn>
    <div class="resultado">
      <p v-if="isValid === undefined">Digite um CPF</p>
      <p v-if="isValid === true">CPF válido</p>
      <p v-if="isValid === false">CPF inválido</p>
    </div>

  </v-sheet>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 80vh;
  background: #0a4e50;
  border-radius: 25px;
  padding: 16px;
}

.title {
  color: #fff;
  font-size: 2rem;
  margin: 0;
}

.subtitle {
  color: #fff;
  font-size: 1.2rem;
  margin: 0;
  text-align: center;
}

.validateButton {
  margin-top: 10px;
  padding: 10px;
  border-radius: 5px;
  border: none;
  background-color: rgba(0, 139, 139, 0.73);
  cursor: pointer;
  color: #fff;
  transition: background-color 0.2s ease-in-out;
}

.validateButton:hover {
  background-color: darkcyan;
}

.resultado {
  margin-top: 10px;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
  background-color: #eee;
  width: 100%;
  font-size: 1.2rem;
  text-align: center;
}

.resultado p {
  margin: 0;
  color: #000;
}
</style>