<script setup>
import { computed, ref } from 'vue';
import ListComponent from './ListComponent.vue';

const newList = ref('');
const currentdate = new Date();
const searchQuery = ref('');

const todoList = ref([]);

const handleNewList = () => {
    const dateToday = currentdate.getFullYear() + '-' + currentdate.getDate() + '-' + currentdate.getDay();
    const listId = Math.floor(Math.random() * 1000)
    todoList.value.push({list_id: listId, list_todo: newList.value, list_date: dateToday, list_status: 0})
    newList.value = ''
};

const getActionFrom = (id, option) => {
    console.log(id)
    const listIndex = todoList.value.findIndex(item => item.list_id === id)
    if (option === 'remove') {
        if (listIndex !== -1) {
            todoList.value.splice(listIndex, 1);
        }
    } else {
        const listStatus = todoList.value[listIndex].list_status;
        todoList.value[listIndex].list_status = listStatus === 0 ? 1 : 0;
    }
};

const searchList = computed(() => {
    const searchTerm = searchQuery.value.toLowerCase()
    return todoList.value.filter(item => item.list_todo.toLowerCase().includes(searchTerm));
});

const handleClearList = () => {
    todoList.value = [];
};

</script>

<template>
    <div class="container">
        <div class="top-container">
            <div class="inputs">
                <label for="input_list">Add new list</label>
                <div class="button">
                    <input type="text" placeholder="Add new list" v-model="newList" id="input_list" @keyup.enter="handleNewList"/>
                    <input type="button" value="Add" @click="handleNewList"/>
                </div>
            </div>
        </div>
        <div class="search-list">
            <label for="search-list">Search</label>
            <div class="search-term">
                <input type="text" placeholder="Search..." id="search-list" v-model="searchQuery" />
                <input type="button" value="Clear List" v-if="todoList.length > 0" @click="handleClearList"/>
            </div>
        </div>
        <div class="bottom-container">
            <ListComponent v-for="index in searchList" :key="index" v-bind="index" @sendActionTo="getActionFrom" />
        </div>
    </div>
</template>


<style scoped>
.container {
    display: flex;
    flex-direction: column;
}
.container .top-container {
    display: flex;
    align-items: center;
    gap: 5px;
}

.top-container .inputs, .search-list {
    display: flex;
    flex-direction: column;
    gap: 5px;
}

.search-list {
    margin-top: 1em;
}


.inputs label, .search-term label {
    font-size: 16px;
    color: #1b1b1b;
}

.inputs input, .search-list input {
    padding: 5px 15px;
    font-size: 18px;
    border-radius: 5px;
    border: 1px solid #000;
}

.button, .search-list {
    display: flex;
    align-items: center;
    gap: 5px;
}

.button input[type="button"] {
    padding: 5px 10px;
}

.bottom-container {
    margin-top: 1em;
    overflow-y: scroll;
    height: calc(100vh - 165px);
}
</style>