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

const deleteCard = (cardIndex, listIndex) => {
    lists[listIndex].cards.splice(cardIndex, 1)
}

const deleteList = (listIndex) => {
    lists.splice(listIndex, 1)
}

const updateCardTitle = (cardIndex, listIndex, newTitle) => {
    lists[listIndex].cards[cardIndex].title = newTitle
}

</script>

<template>

<div class="board">
    <kanbanColumn
    v-for="(list, index) in lists"
    :list="list" :key="list.id"
    @update-list-title="(title) => updateListTitle(index, title)"
    @create-card="(name) => createCard(index, name)"
    @delete-list="() => deleteList(index)"
    @delete-card="(cardIndex) => deleteCard(cardIndex, index)"
    @update-card-title="(cardIndex, newTitle) => updateCardTitle(cardIndex, index, newTitle)"
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
    column-gap: 24px;
    display: flex;
    flex-direction: row;
    width: 100%;
    height:1000px;
    justify-content: flex-start;
}


</style>