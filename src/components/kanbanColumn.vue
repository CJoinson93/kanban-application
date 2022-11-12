<script setup>
import { ref } from 'vue'
import addCardVue from './addCard.vue'
import cardVue from './card.vue'
import cardEntryForm from './cardEntryForm.vue'
import Modal from './Modal.vue'

const isModalOpen = ref(false)

const openModal = () => {
  isModalOpen.value = true
}

const closeModal = () => {
    isModalOpen.value = false
}

const listItems = ref([])
const todo = ref('')
const addToList = () => {
    listItems.push({
        task:todo.value,
    })
}

</script>

<template>

<div id="column">
    <div class="columnTitle"><h2>To Do</h2></div>
    <!--<addCardVue></addCardVue>-->
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


    <cardVue></cardVue>
</div>

</template>

<style scoped>

#column{
    display: flex;
    flex-direction: column;
    row-gap: 16px;
    margin-top:100px;
    margin-left:20px;
    height:100%;
    width:300px;
}

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