<script setup>

import iconClose from './icons/iconClose.vue';

const emit = defineEmits(['close-modal'])

const props = defineProps({
    open: {
        type: Boolean,
        default: false
    }
})

const close = () => {
    emit('close-modal')
}

</script>

<template>
<div v-if="open" class="modal-background" @click="$emit('close')">
    <div class="modal">
        <div class="modal-heading">
            <slot name="header"></slot>
            <iconClose @click="close"/>
        </div>
        <div class="modal-body">
            <slot name="body"></slot>
        </div>
    </div>
</div>

</template>

<style scoped>
.modal-background{
    background: rgba(0, 0, 0, 0.5);
    width: 100%;
    height:100vh;
    position:fixed;
    top:0;
    left:0;
}

.modal{
    margin: 200px auto;
    background: white;
    padding:10px;
    width: 600px;
    border-radius: 10px;
}

.modal-heading{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
}



</style>