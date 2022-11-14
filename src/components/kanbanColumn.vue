<script setup>
import { ref } from 'vue'
import cardVue from './card.vue'
import Modal from './Modal.vue'

//Model Script
const isModalOpen = ref(false)
const openModal = () => {
  isModalOpen.value = true
}
const closeModal = () => {
    isModalOpen.value = false
}

//Add a new card

</script>

<template>

  <div id="column">
      <div class="columnTitle">
        <slot name="col-head"></slot>
      </div>

      <!--New Card Button-->
        <button @click="openModal" class="addCard">+</button>

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
          <button @click="closeModal, addToList">Submit</button>
        </form>
      </template>
    </modal>
    
    <cardVue></cardVue>

  </div>

</template>

<style scoped>

#column{
    display: flex;
    flex-direction: column;
    row-gap: 16px;
    margin-top:100px;
    height:100%;
    width:300px;
}

.addCard{
    width: 100%;
    height:50px;
    background-color: #7FBCD2;
    color: white;
    border:none;
}

:hover.addCard{
    background-color: darkgrey;
}

input, textarea{
    padding:1rem;
    width: 90%;

}
.input-group label{
    display: block;
}


</style>