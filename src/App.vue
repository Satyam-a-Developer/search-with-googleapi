<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
</script>

<template>
  <div class="wrapper">
    <HelloWorld msg="You did it!" />

    <nav>
      <!-- <RouterLink to="/">Home</RouterLink> -->
      <RouterLink to="/">Home</RouterLink>
      <RouterLink to="/about">Saved</RouterLink>
    </nav>
  </div>

  <RouterView />
</template>

<style scoped>
nav {
  width: 100%;
  display: flex;
  justify-content: center;
  font-size: 30px;
  text-align: center;
  margin-top: 2rem;
}
nav a.router-link-exact-active {
  color: rgb(0, 255, 238);
  text-decoration: none;
}

nav a {
  text-decoration: none;
  background-color: black;
  margin: 10px;
  border-radius: 10px;
  padding: 20px;
}
</style>
