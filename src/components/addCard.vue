<script setup>

import { ref } from 'vue'
import Modal from './Modal.vue'
import cardEntryForm from './cardEntryForm.vue';

const props = defineProps ({
    task: String,
})

const isModalOpen = ref(false)

const openModal = () => {
  isModalOpen.value = true
}

const closeModal = () => {
    isModalOpen.value = false
}

</script>

<template>

<button @click="openModal" class="addCard">+</button>

<modal :open="isModalOpen"  @close-modal="closeModal">
    <template #header>
      <h1>Add a New Card</h1>
    </template>
    <template #body>
      <p>Body</p>
      <cardEntryForm></cardEntryForm>
    </template>
  </modal>

</template>

<style scoped>

.addCard{
    width: 100%;
    height:50px;
    background-color: lightgrey;
    color: white;
    border:none;
}

:hover.addCard{
    background-color: darkgrey;
}

</style>