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
    <form @submit.prevent="addTodo">

        <div class="call-button-container">
            <input v-model="newTodo">
        </div>
        <div class="call-button-container">
            <button>Add</button>
        </div>
    </form>
    <div class="background-image"></div>
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
        width: 233px;
        height: 74px;
        vertical-align: middle;
        padding: 10px;
        background: #29A3D8;
        -webkit-border-radius: 4px;
        -moz-border-radius: 4px;
        border-radius: 20px;
        font-family: lato-bold;
        font-size: 17px;
        color: white;
    }
    .background-image {
        content: url(https://i.hizliresim.com/2bs63np.png);
        width: 100%;
        height: 500px;
        object-fit: cover;
    }
    .input_style {
        border-radius: 20px;
        height: 200px;
        color: cornflowerblue;

    }
</style>