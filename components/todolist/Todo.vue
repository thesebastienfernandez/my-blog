<template>
    <main class="todo">
        <div class="todo-header">
            <span id="todo-header-content"><h3>{{ props.title.toUpperCase() }}</h3> <p>Date de cration : {{ props.date }}</p></span>
            <div id="todo-header-buttons">
                <UButton color="gray" label="Modifier" @click="open()" />
                <UModal v-model="isOpen">
                    <UCard :ui="{ ring: '', divide: 'divide-y divide-gray-100 dark:divide-gray-800' }">
                        <template #header>
                                <UInput v-model="title" placeholder="Titre"/>
                        </template>
                        <UTextarea v-model="content" placeholder="Description" />
                        <template #footer>
                            <USelect placeholder="Type de tâche" v-model="type" :options="categories"/>
                            <UButton label="Valider" @click="update(title, content, type)" :disabled="!isValidable" />
                        </template>
                    </UCard>
                </UModal>
                <UButton label="Supprimer" color="red" @click="remove()" />
            </div>
        </div>
        <div class="todo-main">
            <p>{{ props.content }}</p>
        </div>
    </main>
</template>

<script setup>
import {ref} from "vue"
const props = defineProps({
    title: String,
    content: String,
    date: String,
    done: Boolean,
    type: String,
    id: Number
})
const categories = ["matin", "jour", "soir"]
const isOpen = ref(false)
const title = ref(props.title)
const content = ref(props.content)
const type = ref(props.type)
const isValidable = computed(() => {
    return (title.value !== "" && type.value !== "")
})
const emits = defineEmits([
    "updated", "removed"
])

const open = () => {
    isOpen.value = true
}

const remove = () => {
    emits("removed", props.id)
}
const update = (title, content, type) => {
    emits("updated", props.id, title, content, type)
}
</script>

<style scoped>
.todo-header {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: flex-start;
    padding: 0.5em;
    height: 7em;
    background-color: #95a5a6;
    color: white;
}
#todo-header-buttons {
    margin: auto;
    width: 100%;
    display: flex;
    justify-content: space-between;
}
.todo-main {
    padding: 0.5em;
    background-color: #ecf0f1;
}
</style>