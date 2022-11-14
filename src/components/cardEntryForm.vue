<script setup>
import { ref } from 'vue'
import kanbanColumnVue from './kanbanColumn.vue';

const title = ref('')

defineProps (['title'])
defineEmits (['update:title'])
</script>


<template>

    <form>

        <div class="input-group">
            <label for="title">Task Title</label>
            <input v-model="title" type="text" name="title">
        </div>
        <div class="input-group">
            <label for="title">Task Description</label>
            <textarea name="description"></textarea>
        </div>
        <button @click="addToList">Submit</button>

    </form>

 
</template>

<style scoped>

input, textarea{
    padding:1rem;
    width: 90%;

}
.input-group label{
    display: block;
}


</style>