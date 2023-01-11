<script setup>
    import { ref, computed } from 'vue'

    let id = 0

    const newTodo = ref('')
    const hideCompleted = ref(false)
    const todos = ref([
        { id: id++, text: 'Is bulunacak', done: true },
        { id: id++, text: 'Evlenilecek', done: true },
        { id: id++, text: 'Sayginlik', done: false }
    ])

    const filteredTodos = computed(() => {
        return hideCompleted.value
            ? todos.value.filter((t) => !t.done)
            : todos.value
    })

    function addTodo() {
        todos.value.push({ id: id++, text: newTodo.value, done: false })
        newTodo.value = ''
    }

    function removeTodo(todo) {
        todos.value = todos.value.filter((t) => t !== todo)
    }
</script>

<template>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="https://www.w3schools.com/w3css/4/w3.css">
    <div class="background-image"></div>
    <header class="w3-display-container w3-content w3-center" style="max-width:1500px">
        <div class="w3-bar w3-transparent w3-round w3-display-bottommiddle w3-hide-small" style="bottom:-32px">
            <form @submit.prevent="addTodo">
                <div>
                    <input v-model="newTodo" class="call-button-container">
                    <div class= "blank"></div>
                    <button class="add-button">Add</button>
                </div>




</form>
        </div>
    </header>
    <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
            <input type="checkbox" v-model="todo.done">
            <span :class="{ done: todo.done }">{{ todo.text }}</span>
            <button @click="removeTodo(todo)">X</button>
        </li>
    </ul>
    <button @click="hideCompleted = !hideCompleted">
        {{ hideCompleted ? 'Show all' : 'Hide completed' }}
    </button>


</template>

<style>
    .done {
        text-decoration: line-through;
        justify-content: center;
    }
    .button {
        color: red;
    }
    .call-button-container {
        margin: auto;
        width: 643px;
        height: 74px;
        vertical-align: middle;
        padding: 2px;
        background: white;
        border-radius: 36px;
        font-family: lato-bold;
        font-size: 38px;
        border: 2px solid rgba(0, 0, 0, 0.1);
        background-color: white;
        box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    }
    .background-image {
        content: url(https://i.hizliresim.com/2bs63np.png);
        width: 100%;
        height: 480px;
        object-fit: cover;
    }
    .input_style {
        border-radius: 25px;
        background: #73AD21;
        padding: 20px;
        width: 200px;
        height: 150px;
    }
    .add-button {
        margin: auto;
        height: 74px;
        width: 74px;
        color: black;
        border-radius: 37px;
        background: black;

    }
    .blank {
        margin: auto;
        height: 74px;
        width: 2px;
        color: black;
    }
</style>