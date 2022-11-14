<script setup>
import { ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import appHeader from './components/kanbanHead.vue'
import board from './components/kanbanBoard.vue'
</script>

<template>

  <header>
    <appHeader />
  </header>
  <main>
    <board />
  </main>
  <footer>

  </footer>

  <!--<RouterView />-->
</template>

<style scoped>


</style>
