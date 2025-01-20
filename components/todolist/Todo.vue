<template>
    <main class="todo">
        <div class="todo-header">
            <h3>{{ props.title }}</h3> <p>{{ props.date }}</p> <p>{{ props.type }}</p>
            <UButton label="Modifier" @click="open()" />
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
            <!-- <Modal label="Modifier" :title="props.title" :content="props.content" :type="props.type" @validated="(title, content, type) => update(title, content, type)" /> -->
            <UButton label="Supprimer" @click="remove()" />
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
const categories = ["work", "home", "biohack"]
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
.todo {
    background-color: greenyellow;
}
.todo-header {
    background-color: brown;
}
.todo-main {
    background-color: aquamarine;
}
</style>