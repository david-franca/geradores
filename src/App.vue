<script setup lang="ts">
import {RouterLink, RouterView} from 'vue-router'
import Menu from './components/MenuNav.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <Menu title="Geradores"/>

      <nav>
        <RouterLink to="/">CPF</RouterLink>
        <RouterLink to="/validate">Validador de CPF</RouterLink>
        <RouterLink to="/password">Senha</RouterLink>
      </nav>
    </div>
  </header>

  <div class="router">
    <RouterView/>
  </div>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
  width: 100vw;
  padding-bottom: 8px;
}

header .wrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}

header .wrapper :nth-child(1) { order: 2; }
header .wrapper :nth-child(2) { order: 3; }
header .wrapper :nth-child(3) { order: 1; }

.router {
  width: 100vw;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
    width: 50vw;
  }

  .router {
    width: 40vw;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
