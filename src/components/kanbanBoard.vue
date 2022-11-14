<script setup>
import kanbanColumn from './kanbanColumn.vue'

</script>

<template>

<div class="board">
    <kanbanColumn>
        <template #col-head>
            <h2>To Do</h2>
        </template>
    </kanbanColumn>

    <kanbanColumn>
        <template #col-head>
            <h2>In Progress</h2>
        </template>
    </kanbanColumn>

    <kanbanColumn>
        <template #col-head>
            <h2>Check it Over</h2>
        </template>
    </kanbanColumn>

    <kanbanColumn>
        <template #col-head>
            <h2>Completed</h2>
        </template>
    </kanbanColumn>
</div>

</template>

<style scoped>

.board{
    left:0;
    column-gap: 8px;
    display: flex;
    flex-direction: row;
    width: 100%;
    height:1000px;
    background-color: #FFEEAF;
    justify-content: space-evenly;
}


</style>