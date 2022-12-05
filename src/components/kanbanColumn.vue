<script setup>

import { ref } from 'vue'
import cardVue from './card.vue'
import Modal from './Modal.vue'
import addCardVue from './addCard.vue'
import iconDelete from './icons/iconDelete.vue'

const emit = defineEmits(['update-list-title', 'delete-list'])
const editing = ref(false)
const listTitleEdit = ref(null)

const props = defineProps(
  {
    list: {
      type: Object,
    }
  }
)

const edit = () => {
  editing.value = true
}

const saveEdit = () => {
  emit('update-list-title', listTitleEdit.value.value)
  editing.value = false
}

const deleteList = () => {
  let reallyDelete = confirm('Are you shure you want to delete this list?')
  
  if (reallyDelete){
    emit('delete-list')
  }

}

</script>

<template>

  <div id="column">
      <div class="columnTitle">
        <h2 @click="edit">{{editing ? '&nbsp;' : list.title }}</h2>
        <div class="delete" @click="deleteList">
        <iconDelete />
        </div>
        <input
          v-if="editing"
          class="list__header-input"
          type="text"
          @change="saveEdit"
          :value="list.title"
          ref="listTitleEdit"
        />

       <!-- <slot name="col-head"></slot>-->
      </div>

      <addCardVue
        @create="(name) => $emit('create-card', name)"
      ></addCardVue>
      
      
      
      <cardVue
        v-for="(card, cardId) in list.cards"
        :key="card.id"
        :card="card"
        @delete-card="$emit('delete-card', cardId)"
        @update-card-title="(title) => $emit('update-card-title', cardId, title)"
        @update-card-description="(description) => $emit('update-card-description', index, description)"
      ></cardVue>

  </div>

</template>

<style scoped>

#column{
    display: flex;
    flex-direction: column;
    row-gap: 16px;
    height:100%;
    width:250px;
}

.columnTitle{
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
}

.list__header-input{
  position: absolute;
  width: 250px;
  height:30px;
  background: rgb(198, 198, 198);
  border: none;
  font-size: 28px;
}

.delete{
  width:24px;
  height:24px;
  cursor: pointer;
}

</style>