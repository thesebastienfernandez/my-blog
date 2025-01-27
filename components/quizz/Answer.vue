<template>
    <label :for="id" :class="classes">
        <input :disabled="disabled" type="radio" name="answer" :id="id" v-model="model" :value="value">
        {{ value }}
    </label>
</template>

<script setup>
import {computed} from "vue"
const props = defineProps({
    id: String,
    disabled: Boolean,
    value: String,
    correctAnswer: String

})
const model = defineModel()
const classes = computed(() => ({
    disabled: props.disabled,
    right: props.disabled && props.value === props.correctAnswer,
    wrong: props.disabled && props.value !== props.correctAnswer && model.value === props.value
}))
</script>

<style scoped>
.disabled {
    opacity: .5;
}
.right {
    opacity: 1;
    color: #2ecc71;
}
.wrong {
    opacity: 1;
    color: red;
}
</style>

