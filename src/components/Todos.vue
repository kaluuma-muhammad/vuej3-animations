<template>
    <div class="todos">
        <input type="text" v-model="newTodo" @keypress.enter="addTodo" placeholder="Add new todo...">
        <transition name="switch" mode="out-in">
            <div v-if="todos.length">
                <transition-group tag="ul" name="list" appear>
                    <li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
                        {{ todo.text }}
                    </li>
                </transition-group>
            </div>
            <div v-else="">Opps! There are no todos available</div>
        </transition>
    </div>
</template>

<script>
    import { ref } from 'vue'

    export default {
        name: 'Todos',
        setup(props, { emit }) {
            const newTodo = ref('')
            const todos = ref([
                { id: 1, text: 'Make the bed'},
                { id: 2, text: 'Wake up and code'}
            ])

            const addTodo = () => {
                if (newTodo.value) {
                    const id = Math.random()
                    todos.value = [
                        { text: newTodo.value, id},
                        ...todos.value
                    ]
                    newTodo.value = ''
                } else {
                    emit('badValue')
                }
            }

            const deleteTodo = (id) => {
                todos.value = todos.value.filter(todo => todo.id != id)
            }

            return { todos, addTodo, deleteTodo, newTodo }
        }
    }
</script>

<style>
    .todos {
        max-width: 400px;
        margin: 20px auto;
        position: relative;
    }

    input {
        width: 100%;
        padding: 12px;
        border: 1px solid #eee;
        border-radius: 10px;
        box-sizing: border-box;
        margin-bottom: 20px;
    }

    .todos ul {
        position: relative;
        padding: 0;
    }

    .todos li {
        list-style-type: none;
        display: block;
        margin-bottom: 10px;
        padding: 10px;
        background: white;
        box-shadow: 1px 3px 5px rgba(0,0,0,0.1);
        border-radius: 10px;
        width: 100%;
        box-sizing: border-box;
    }

    .todos li:hover {
        cursor: pointer;
    }

    /* list transitions */
    .list-enter-from, .list-leave-to {
        opacity: 0;
        transform: scale(0.6);
    }
    .list-enter-to, .list-leave-from {
        opacity: 1;
        transform: scale(1);
    }
    .list-enter-active {
        transition: all 0.4s ease;
    }
    .list-leave-active {
        transition: all 0.4s ease;
        position: absolute;
    }
    .list-move {
        transition: all 0.3s ease;
    }

    /* switch transitions */
    .switch-enter-from, .switch-leave-to {
        opacity: 0;
        transform: translateY(20px);
    }
    .switch-enter-active, .switch-leave-active {
        transition: all 0.5s ease;
    }
</style>
