<script setup lang="ts">
defineProps<{
  title: string
}>()
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ title }}</h1>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1 {
  text-align: center;
  display: none;
}

@media (min-width: 1024px) {
  .greetings h1 {
    text-align: left;
    display: block;
  }
}
</style>
