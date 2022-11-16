<script setup>

import { ref } from 'vue';
import Modal from './Modal.vue';
import { Transition } from 'vue';

const props = defineProps({
    card: {
        type: Object,
    },
    
})

//Model Script
const isModalOpen = ref(false)
const openModal = () => {
  isModalOpen.value = true
}
const closeModal = () => {
    isModalOpen.value = false
}

</script>

<template>

<div class="card" @click="openModal"> 
    
    <p> {{title}} </p>

</div>

<!--Model-->
<Transition>
<modal :open="isModalOpen"  @close-modal="closeModal">
      <template #header>
        <h2>Card Content</h2>
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
</Transition>
</template>

<style scoped>

.card{
    width:100%;
    background-color: #A5F1E9;
    height:40px;
    border-radius: 10px;
}

input, textarea{
    padding:1rem;
    width: 90%;

}
.input-group label{
    display: block;
}

/* Transitions */
.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}

</style>