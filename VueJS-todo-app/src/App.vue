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
                    <button class="add-button">
                        Add
                    </button>
                </div>




</form>
        </div>
    </header>
    <ul>
        <div class="mid-blank"></div>
        <ul v-for="todo in filteredTodos" :key="todo.id">

            <div class="todo-note">
                <input type="checkbox" v-model="todo.done" class="my-checkbox-x2" value="1" />
                <div class="note-style-i">

                    <span :class="{ done: todo.done }">{{ todo.text }}</span>
                </div>
            </div>
</ul>
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
        margin-left: 10px;
        vertical-align: middle;
        padding: 2px;
        background: white;
        border-radius: 36px;
        font-family: Arial;
        font-size: 38px;
        border: 2px solid rgba(0, 0, 0, 0.1);
        background-color: white;
    }
    .todo-note {
        margin: auto;
        margin-top: 20px;
        width: 643px;
        height: 74px;
        vertical-align: middle;
        padding: 2px;
        background: white;
        border-radius: 32px;
        font-family: Arial;
        font-size: 26px;
        border: 2px solid rgba(0, 0, 0, 0.1);
        background-color: white;
        box-shadow: rgba(0, 0, 0, 0.24) 10px 3px 18px;
        list-style: none;
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
        margin-left: 20px;
        height: 74px;
        width: 74px;
        color: black;
        border-radius: 37px;
        background: black;
    }
    .note-style {
        margin-left: 20px;
        font-family: lato-bold;
        font-size: 20px;
    }
    .mid-blank {
        margin-top: 100px;
    }
    .note-style-i {
        margin-top: 15px;
        text-align: center;
    }

    .my-checkbox-x2 {
        position: absolute;
        transform: scale(5);
        margin: 26px 10px 0 0;
        margin-left: 50px;
        accent-color: #34495e;
    }



</style>