<script setup>
import kanbanColumn from './kanbanColumn.vue'

</script>

<template>

<div class="board">

    <kanbanColumn></kanbanColumn>x
</div>

</template>

<style scoped>

.board{
    left:0;
    display: flex;
    flex-direction: row;
    column-gap: 20px;
    flex-wrap: nowrap;
    width: 100%;
    height:1000px;
    background-color: lightblue;
}


</style>