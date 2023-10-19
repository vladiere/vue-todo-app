<template>
    <ul>
        <li :key="id">
            <span class="list">
                <span>{{ list_name }}</span>
                <span>{{ date_time }}</span>
            </span>
            <span class="done">{{ list_status === 0 ? 'Done' : 'Undone' }}</span>
            <span class="remove">Remove</span>
        </li>
    </ul>
</template>

<script setup>

const { id, list_name, date_time, list_status} = defineProps({
    id: {
        type: Number,
        default: 0,
    },
    list_name: {
        type: String,
        default: "",
    },
    date_time: {
        type: String,
        default: "",
    },
    list_status: {
        type: Number,
        default: 0
    }
})

</script>

<style scoped>
ul {
    border-bottom: 2px solid #000;
    padding: 0px 15px;
}

ul li {
    list-style: none;
    display: flex;
    align-items: center;
    gap: 15px;
}

li .list {
    display: flex;
    flex-direction: column;
    margin-right: 5em;
}

.list span:nth-child(2) {
    font-size: 12px;
    color: gray;
}
li .done, li .remove {
    cursor: pointer;
    padding: 5px;
    border-radius: 5px;
    font-size: 14px;
}

.done {
    background-color: lime;
}

.remove {
    background-color: red;
    color: whitesmoke;
}
</style>