<script setup>

import { ref } from 'vue'
import Modal from './Modal.vue'

//Model Window
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
        <form>
          <div class="input-group">
            <label for="colTitle">Title</label>
            <input type="text" name="colTitle">
          </div>
        </form>
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

input, textarea{
    padding:1rem;
    width: 90%;

}
.input-group label{
    display: block;
}

</style>