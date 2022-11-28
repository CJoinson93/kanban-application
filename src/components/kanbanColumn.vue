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
  emit('delete-list')
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
        v-for="(card, index) in list.cards"
        :key="card.id"
        :card="card"
        @delete-card="$emit('delete-card', index)"
        @update-card-title="(title) => $emit('update-card-title', index, title)"
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

.delete{
  width:24px;
  height:24px;
  cursor: pointer;
}

</style>