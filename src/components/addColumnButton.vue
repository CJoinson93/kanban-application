<script setup>

import { ref } from 'vue'
import Modal from './Modal.vue'
import iconMore from './icons/iconMore.vue';

const emit = defineEmits(['create'])

const name = ref (null)
const editing = ref(false)

const create = () => {
  emit('create')
}


</script>

<template>
  <div class="addColumn">
    <a class="newColumnButton" href="#" @click.prevent="create">
      <iconMore/>
      Add Column
    </a>
  </div>
</template>

<style scoped>

.addColumn{
    margin-top: 53px;
    width:200px;
    height:40px;
    background-color: #4f7380;
    border: none;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
}

.newColumnButton{
  display: flex;
  width: 100%;
  justify-content: center;
  align-items: center;
  height:100%;
}

:hover.addColumn{
  background-color: #7FBCD2;
}

a{
  color: white;
  text-decoration: none;
}



</style>