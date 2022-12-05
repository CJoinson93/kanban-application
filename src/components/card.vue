<script setup>

import { onMounted, ref } from 'vue';
import Modal from './Modal.vue';
import { Transition } from 'vue';
import axios from 'axios';

const props = defineProps({
    card: {
        type: Object,
    },
    
})

const emit = defineEmits(['delete-card','update-card-title'])

//Model Script
const isModalOpen = ref(false)
const openModal = () => {
  isModalOpen.value = true
}
const closeModal = () => {
    isModalOpen.value = false
    editingTitle.value = false
}

const saveTitle = () => {
  emit('update-card-title', cardTitleEdit.value.value)
  editingTitle.value = false
}

const deleteCard = () => {
  let reallyDelete = confirm('Are you sure you want to delete this card?')

  if (reallyDelete) {
      emit('delete-card')
  }
}

const updateCardTitle = (cardId, listIndex, newTitle) => {
    axios.patch(`${baseUrl}/cards/${cardId}`,{
        title: newTitle,
    }
    )
    .then((resp) => {
        for (let i = 0; i < lists.value[listIndex].cards.length; i++) {
            if (lists.value[listIndex].cards[i].id == cardId) {
                lists.value[listIndex].cards[i].title = resp.data.data.title
                break
            }
        }
    })
}

const editingTitle = ref(false)
const cardTitleEdit = ref(null)

</script>

<template>

<div class="card" @click="openModal"> 
    
    {{ card.title }}

</div>

<!--Model-->
<Transition>

<modal :open="isModalOpen"  @close-modal="closeModal">
  <template #header>
    <h2 @click="editingTitle = true">{{ card.title }}</h2>
    <input 
      v-if="editingTitle" 
      :value="card.title" 
      type="text" 
      class="editor__title" 
      ref="cardTitleEdit"
      @update-card-title="(cardId, newTitle) => updateCardTitle(cardId, index, newTitle)"
      @keypress.enter="saveTitle"     
    />
  </template>
    
  <template #body>
    {{card.content}}
  </template>

  <template #footer>
    <button id="delete" @click="deleteCard">Delete</button>
  </template>

</modal>

</Transition>
</template>

<style scoped>

.editor__title{
  position: absolute;
  width:100%;
  font-size:28px;
  background: rgb(198, 198, 198);
  top:0;
  left:0;
  border:none;
}

.card{
    width:100%;
    background-color: #A5F1E9;
    height:40px;
    border-radius: 5px;
    display: flex;
    flex-direction: row;
    justify-items: center;
    justify-content: center;
    padding-top: 15px;
}

#delete{
  background-color: red;
  border: none;
  padding: 10px;
  color: white;
  border-radius: 5px;
}

/*input, textarea{
    padding:1rem;
    width: 90%;

}*/
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