<script setup>

import { ref } from 'vue'
import cardVue from './card.vue'
import Modal from './Modal.vue'
import addCardVue from './addCard.vue'

const emit = defineEmits(['update-list-title'])
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

</script>

<template>

  <div id="column">
      <div class="columnTitle">
        <h2 @click="edit">{{editing ? '&nbsp;' : list.title }}</h2>
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
        v-for="card in list.cards"
        :key="card.id"
        :card="card"
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

</style>