<script setup>

import { ref } from 'vue'
import Modal from './Modal.vue'



//Trying to add a new card
const props = defineProps ({
    task: String,
})

//Model Open & close
const isModalOpen = ref(false)
const openModal = () => {
  isModalOpen.value = true
}
const closeModal = () => {
    isModalOpen.value = false
}

</script>

<template>

<!--Adding a Card Button-->
  <button @click="openModal" class="addCard">+</button>

<!--Model for adding a card-->  
    <modal :open="isModalOpen"  @close-modal="closeModal">
      <template #header>
        <h1>Add a New Card</h1>
      </template>
      
      <template #body>
        <form>
          <div class="input-group">
            <label for="title">Task Title</label>
              <input v-model="title" type="text" name="title">
          </div>
          <div class="input-group">
            <label for="title">Task Description</label>
            <textarea name="description"></textarea>
          </div>
          
          <button @click="">Submit</button>
        </form>    
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