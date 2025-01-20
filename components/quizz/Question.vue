<template>
    <div class="question">
        <h3>{{ question.question }}</h3>
        <ul>
            <li v-for="(choice, index) in randomChoices" :key="choice">
                <Answer :id="`answer${index}`" :disabled="answer" :value="choice" v-model="answer" :correctAnswer="question.good_answer"/>
            </li>
        </ul>
        <button :disabled="!answer" @click="emits('answer', answer)">Question suivante</button>
    </div>
</template>

<script setup>
import { computed } from 'vue';
import { shuffleArray } from './functions/array';
import Answer from './Answer.vue';
const props = defineProps({
    question: Object
})
const emits = defineEmits(["answer"])
const answer = ref(null)
const randomChoices = computed(() => {
    return shuffleArray(props.question.choices)
})
</script>
<style scoped>
.question {
    padding-top: 2rem;
}
.question button {
    margin-left: auto;
    display: block;
}
</style>