<script setup>
import { v4 as uuid } from 'uuid'
import { reactive } from 'vue'
import addColumnButtonVue from './addColumnButton.vue';

import kanbanColumn from './kanbanColumn.vue'

const lists = reactive(
    [
        {
            id:uuid(),
            title:'To do',
            cards:
            [
                {
                    id:uuid(),
                    title:'My first card',
                    content:'This is the content'
                }
            ]
        }
    ]
)

const createList = () => {
    lists.push({
        id:new uuid(),
        title: 'New List',
        cards:[],
    })
}

const updateListTitle = (listIndex, newTitle) => {
    lists[listIndex].title = newTitle
}

const createCard = (listIndex,title) => {
    lists[listIndex].cards.push({
        id: uuid(),
        title: title,
    })
}

</script>

<template>

<div class="board">
    <kanbanColumn
    v-for="(list, index) in lists"
    :list="list" :key="list.id"
    @update-list-title="(title) => updateListTitle(index, title)"
    @create-card="(name) => createCard(index, name)"
    ></kanbanColumn>

    <addColumnButtonVue
    @create="createList"
    ></addColumnButtonVue>

</div>

</template>

<style scoped>

.board{
    left:0;
    margin-top:80px ;
    padding:20px;
    column-gap: 8px;
    display: flex;
    flex-direction: row;
    width: 100%;
    height:1000px;
    justify-content: flex-start;
}


</style>