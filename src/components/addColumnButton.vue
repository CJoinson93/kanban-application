<script setup>

import { ref } from 'vue'
import Modal from './Modal.vue'
import columnEntryForm from './columnEntryForm.vue';

const isColumnModalOpen = ref(false)

const openModal = () => {
  isColumnModalOpen.value = true
}

const closeModal = () => {
    isColumnModalOpen.value = false
}


</script>

<template>

<button id="addColumn" @click="openModal">Add More</button>

<modal :open="isColumnModalOpen"  @close-modal="closeModal">
    <template #header>
      <h1>Add a New Column</h1>
    </template>
    <template #body>
      <p>Body</p>
      <columnEntryForm></columnEntryForm>
    </template>
  </modal>

</template>

<style scoped>

#addColumn{
    margin-top: 25px;
    width:100px;
    height:30px;
    background-color: black;
    border: none;
    border-radius: 5px;
    color: white;
}

</style>