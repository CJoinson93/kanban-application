<script setup>
import { v4 as uuid } from 'uuid'
import { onMounted, ref } from 'vue'
import axios from 'axios'
import addColumnButtonVue from './addColumnButton.vue';

import kanbanColumn from './kanbanColumn.vue'
const baseUrl = 'http://localhost/api'

const lists = ref([])

onMounted(() => {
    loadListsFromApi()
})

const loadListsFromApi = () => {
    axios.get(`${baseUrl}/todo-lists`)
         .then((response) => {
            const data = response.data.data
            lists.value = data
         })
}


const createList = () => {
    axios.post(`${baseUrl}/todo-lists`, {
        title: 'New List',
    }) .then((response) => {
        const list = response.data.data
        lists.value.push(list)
    })
}

const updateListTitle = (listId, newTitle) => {
    axios.patch(`${baseUrl}/todo-lists/${listId}`,{
        title:newTitle,
    }).then((response) => {
        const data = response.data.data
        const listIndex = getListById(listId)
        lists.value[listIndex].title = data.title
        })
}

const createCard = (listId,title) => {
    axios.post(`${baseUrl}/cards`,{
        title:title,
        todo_list_id:listId,
    }).then((response) => {
        const listIndex = getListById(listId)
        lists.value[listIndex].cards.push(response.data.data)
    })
}

const deleteCard = (cardId, listId) => {
    axios.delete(`${baseUrl}/cards/${cardId}`)
    .then((resp) => {
        for (let i = 0; i <lists.value[listId].cards.length; i++) {
            if (lists.value[listId].cards[i].id == cardId) {
                lists.value[listId].cards.splice (i, 1)
                break
            }
        }

    })
}

const deleteList = (listId) => {
    axios.delete(`${baseUrl}/todo-lists/${listId}`)
    .then((resp) => {
        for (let i = 0; i < lists.value.length; i++) {
            if (lists.value[i].id == listId) {
                lists.value.splice(i, 1)
                break
            }
        }
    })

    .catch((err) => {
        alert('Error deleting list')
    })
    //lists.splice(listIndex, 1)
}

const updateCardTitle = (cardId, listId, newTitle) => {
    axios.patch(`${baseUrl}/cards/${cardId}`,{
        title: newTitle,
    }
    )
    .then((resp) => {
        for (let i = 0; i < lists.value[listId].cards.length; i++) {
            if (lists.value[listId].cards[i].id == cardId) {
                lists.value[listId].cards[i].title = resp.data.data.title
                break
            }
        }
    })
}

const getListById = (id) => {
    for (let i = 0; i <lists.value.length; i++) {
        if (lists.value[i].id == id) {
            return i
        }
    }
}

const updateCardDescription = (cardId, listId, newDescription) => {
    lists[listId].cards[cardId].content = newDescription
}

</script>

<template>

<div class="board">
    <kanbanColumn
    v-for="(list, index) in lists"
    :list="list" :key="list.id"
    @update-list-title="(title) => updateListTitle(list.id, title)"
    @create-card="(name) => createCard(list.id, name)"
    @delete-list="() => deleteList(list.id)"
    @delete-card="(cardId) => deleteCard(cardId, index)"
    @update-card-title="(cardId, newTitle) => updateCardTitle(cardId, index, newTitle)"
    @update-card-description="(cardId, newDescription) => updateCardDescription(cardId, index, newDescription)"
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