<template>
    <h1>Recap</h1>
    <p>
        {{ hasWon ? quiz.succes_message : quiz.failure_message }}
    </p>
    <p>Score : {{ score }}/{{ quiz.questions.length }}</p>
</template>

<script setup>
import { computed } from 'vue';
const props = defineProps({
    answers: Array,
    quiz: Object
})

const score = computed(() => {
    return props.quiz.questions.reduce((acc, question, k) => {
        if(question.good_answer === props.answers[k]) {
            return acc+1
        }
        return acc
    }, 0)
})
const hasWon = computed(() => {
    return props.quiz.minimum_score <= score.value
})
</script>