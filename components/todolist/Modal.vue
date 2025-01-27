<template>
    <UButton size="xl" color="black" :label="props.label" @click="open()" />
    <UModal v-model="isOpen">
        <UCard :ui="{ ring: '', divide: 'divide-y divide-gray-100 dark:divide-gray-800' }">
            <template #header>
                    <UInput v-model="title" placeholder="Titre"/>
            </template>
            <UTextarea v-model="content" placeholder="Description" />
            <template #footer>
                <USelect placeholder="Moment de la routine" v-model="type" :options="categories"/>
                <div class="validation">
                <UButton block size="xl" label="Valider" @click="validation()" :disabled="!isValidable" />
                </div>
            </template>
        </UCard>
    </UModal>
</template>

<script setup>
import { ref, computed } from 'vue';
const categories = ["matin", "jour", "soir"]
const props = defineProps({
    title: String,
    content: String,
    type: String,
    label: String
})
const title = ref(props.title)
const content = ref(props.content)
const type = ref(props.type)
const isOpen = ref(false)
const emits = defineEmits([
    "validated"
])
const open = () => {
    isOpen.value = true
}
const isValidable = computed(() => {
    return (title.value !== "" && type.value !== "")
})
const validation = () => {
    emits("validated", title, content, type)
    isOpen.value = false
}


</script>
<style scoped>
.validation {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 4em;
    margin-top: 2em;
}
</style>