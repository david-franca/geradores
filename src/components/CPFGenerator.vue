<script setup lang="ts">

import {ref} from "vue";

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

function randomize(): string {
  const min: number = 100000000
  const max: number = 999999999
  return Math.floor(Math.random() * (max - min) + min).toString()
}

function format(cpf: string): string {
  return cpf.replace(/(\d{3})(\d{3})(\d{3})(\d{2})/, '$1.$2.$3-$4')
}

function generate() {
  const cpf = randomize()
  const digit1 = generateDigit(cpf)
  const digit2 = generateDigit(cpf + digit1)
  return format(cpf + digit1 + digit2)
}

const cpfRef = ref(generate())

function updateCpf() {
  cpfRef.value = generate()
}

</script>

<template>
  <v-sheet elevation="12"
           height="90vh"
           rounded="lg"
           width="100%"
           class="pa-4 text-center mx-auto bg-teal-darken-3 justify-center align-center d-flex flex-column ">
    <h1>Gerador de CPF</h1>
    <p>{{ cpfRef }}</p>
    <v-btn color="primary" @click="updateCpf">Gerar</v-btn>
  </v-sheet>
</template>

<style scoped>
h1 {
  color: #fff;
  font-size: 2rem;
  margin: 0;
}

p {
  color: #fff;
  font-size: 4rem;
  margin: 0;
  text-align: center;
}
</style>
