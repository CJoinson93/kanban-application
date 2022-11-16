<script setup>

import { ref } from 'vue'
import iconMore from './icons/iconMore.vue';

const emit = defineEmits(['create'])

const name = ref(null)
const creating = ref (false)

const create = () => {
  emit('create')
  name.value = null
  creating.value = ! creating.value
}

const save = () => {
  if (name.value !== null && name.value.trim () !== '') {
    emit('create', name.value)
    name.value = null
    creating.value = false
  }
}

</script>

<template>

<!--Adding a Card Button-->
  <div class="addCard">
    <a class="addCardButton" href="#" @click="create">
      <iconMore/>
      Add Card
    </a>
    <!-- <input v-if="creating" type="text" v-model="name" placeholder="card-title" @keypress.enter="save" /> -->
  </div>

</template>

<style scoped>

.addCard{
  width: 100%;
  height:40px;
  background-color: #7FBCD2;
  color: white;
  border:none;
  display: flex;
  align-items: center;
  justify-content: center;
}

.addCardButton{
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  width:100%;
  height: 100%;
}

:hover.addCard{
    background-color: darkgrey;
}

a {
  color: white;
}

</style>