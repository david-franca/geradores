<script setup lang="ts">
import {ref} from "vue";

const passwordLength = ref(12);
const uppercase = ref(true);
const lowercase = ref(true);
const digits = ref(true);
const symbol = ref(true);
const password = ref(generatePassword())

function generatePassword() {
  const upper = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
  const lower = upper.toLowerCase()
  const number = "0123456789"
  const symbols = "`~!@#$%^&*()-_=+[{]}\\|;:'\",<.>/? ";
  let char = 0
  let all = ''
  let value = ''
  if (uppercase.value) all += upper
  if (lowercase.value) all += lower
  if (digits.value) all += number
  if (symbol.value) all += symbols

  for (let i = 0; i < passwordLength.value; i++) {
    char = Math.floor(Math.random() * all.length)
    value += all.charAt(char)
  }
  return value
}

function handleClick() {
  password.value = generatePassword()
}

</script>
<template>
  <v-sheet elevation="12"
           rounded="lg"
           width="100%"
           class="text-center mx-auto bg-teal-darken-3 justify-center align-center d-flex flex-column ">
    <v-form>
      <v-container>
        <v-row>
          <v-col cols="12">
            <h1 class="mb-4">Gerador de Senha</h1>
          </v-col>
          <v-col cols="12">
            <v-text-field
                v-model="password"
                label="Senha"
                readonly
            ></v-text-field>
          </v-col>
          <v-col cols="12">
            <v-slider
                v-model="passwordLength"
                thumb-label="always"
                label="Tamanho da senha"
                step="1"
                min="6"
            ></v-slider>
          </v-col>
          <v-col cols="6">
            <v-checkbox
                v-model="uppercase"
                label="Letra maiúscula"
            ></v-checkbox>
          </v-col>
          <v-col cols="6">
            <v-checkbox
                v-model="lowercase"
                label="Letra minúscula"
            ></v-checkbox>
          </v-col>
          <v-col cols="6">
            <v-checkbox
                v-model="digits"
                label="Dígitos"
            ></v-checkbox>
          </v-col>
          <v-col cols="6">
            <v-checkbox
                v-model="symbol"
                label="Símbolos"
            ></v-checkbox>
          </v-col>

          <v-col cols="12">
            <v-btn
                color="primary"
                @click="handleClick"
            >Gerar Senha
            </v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
  </v-sheet>
</template>

<style scoped>

</style>
