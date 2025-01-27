<template>
    <div>
        <header>
            <h1>Ma todoList</h1>
        </header>
        <main>
            <Modal label="Ajouter une tâche" title="" content="" type="" @validated="(title, content, type) => addTodo(title, content, type)" />
            <div id="container">
                <section>
                    <h2>Routine du lever</h2>
                    <ul v-if="todos">
                        <li v-for="(todo, index) in todos.list.filter(todo => todo.type === 'matin')" :key="todo.id">
                            <Todo
                                :title="todo.title"
                                :content="todo.content"
                                :date="todo.date"
                                :done="false"
                                :type="todo.type"
                                :id="todo.id"
                                @updated="(id, title, content, type) => updateTodo(id, title, content, type)"
                                @removed="(id) => removeToList(id)"
                            >
                            </Todo>
                        </li>
                    </ul>
                </section>
                <section>
                    <h2>Séance(s) de la journée</h2>
                    <ul v-if="todos">
                        <li v-for="(todo, index) in todos.list.filter(todo => todo.type === 'jour')" :key="todo.id">
                            <Todo
                                :title="todo.title"
                                :content="todo.content"
                                :date="todo.date"
                                :done="false"
                                :type="todo.type"
                                :id="todo.id"
                                @updated="(id, title, content, type) => updateTodo(id, title, content, type)"
                                @removed="(id) => removeToList(id)"
                            >
                            </Todo>
                        </li>
                    </ul>
                </section>
                <section>
                    <h2>Routine avant coucher</h2>
                    <ul v-if="todos">
                        <li v-for="(todo, index) in todos.list.filter(todo => todo.type === 'soir')" :key="todo.id">
                            <Todo
                                :title="todo.title"
                                :content="todo.content"
                                :date="todo.date"
                                :done="false"
                                :type="todo.type"
                                :id="todo.id"
                                @updated="(id, title, content, type) => updateTodo(id, title, content, type)"
                                @removed="(id) => removeToList(id)"
                            >
                            </Todo>
                        </li>
                    </ul>
                </section>
            </div>
        </main>
    </div>
</template>

<script setup>
import Todo from '~/components/todolist/Todo.vue';
import Modal from '~/components/todolist/Modal.vue';
import { onMounted, ref } from 'vue';
const todos = ref(null)
onMounted(() => {
    fetch("./todos.json")
        .then(r => {
            if(r.ok) {
                return r.json()
            }
            throw new Error("Impossible de récupérer le json")
        })
        .then(data => {
            todos.value = data
        })
        .catch((e) => {
            console.error(e)
        })
})
const removeToList = (id) => {
    if (todos) {
        todos.value.list = todos.value.list.filter(todo => todo.id !== id)
    }
    for (let i = 0; i < todos.value.list.length; i++) {
        todos.value.list[i].id = i
    }
}
const updateTodo = (id, title, content, type) => {
    if (todos) {
        for (let i = 0; i < todos.value.list.length; i++) {
           if(todos.value.list[i].id === id) {
            todos.value.list[i].title = title
            todos.value.list[i].content = content
            todos.value.list[i].type = type
           }
            
        }
    }
}
const addTodo = (title, content, type) => {
    console.log("addTodo de : " + title.value)
    if (todos) {
        todos.value.list.push({
        title: title,
        content: content,
        date: "2024-12-19T10:48:00.000Z",
        type: type,
        id: todos.value.list.length,
        done: false
        })
    }
    
    
    
}

</script>

<style scoped>
#container {
    margin: 0 auto;
    margin-top: 2em;
    display: flex;
    width: 100%;
    height: 600px;
}
section {
    width: 33%;
    border-right: 2px solid black;
}
</style>