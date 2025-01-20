<template>
    <main class="container">
        <div v-if="state === 'error'">
            <p>Impossible de charger le quiz</p>
        </div>
        <div :aria-busy="state === 'loading'">
            <div v-if="quiz !== null">
                <Quiz :quiz="quiz" />
            </div>
        </div>
    </main>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import Quiz from './components/quizz/Quiz.vue';

const quiz = ref(null)
const state = ref("loading")
onMounted(() => {
    fetch("./quiz.json")
        .then(r => {
            if(r.ok) {
                return r.json()
            }
            throw new Error("Impossible de récupérer le json")
        })
        .then(data => {
            quiz.value = data
            state.value = "idle"
        })
        .catch((e) => {
            state.value = "error"
        })
})
</script>

<style scoped>
.container {
    margin-top: 2rem;
}
</style>