<script setup>
import { ref } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import appHeader from './components/kanbanHead.vue'
import board from './components/kanbanBoard.vue'

</script>

<template>

  <header>
    <appHeader></appHeader>
  </header>
  <main>
    <board></board>
  </main>
  <footer>

  </footer>

  <!--<RouterView />-->
</template>

<style scoped>


</style>
