<template>
    <div class="question">
        <h3>{{ question.question }}</h3>

        <ul>
            <li v-for="(choice, index) in randomChoices" :key="choice">
                <Answer :id="`answer${index}`" :disabled="hasAnswer" :value="choice" @change="onAnswer"
                    :correctAnswer="question.correct_answer" v-model="answer" />
                {{ value }}
            </li>
        </ul>
    </div>
</template>

<script setup>
import { computed, onMounted, onUnmounted, ref, watch } from 'vue'
import { shuffleArray } from '../array.js'
import Answer from './Answer.vue'

let timer = null
const emits = defineEmits(['answer'])
const answer = ref(null)
const props = defineProps({
    question: Object
})
const hasAnswer = computed(() => answer.value !== null)

const onAnswer = () => {
    clearTimeout(timer)
    timer = setTimeout(() => {
        emits('answer', answer.value)
    }, 1000)
    
}

watch(() => props.question, () => {
    answer.value = null
})
const randomChoices = computed(() => {
    if (!props.question) return []
    return shuffleArray([...props.question.choices])
})


onMounted(() => {
    timer = setTimeout(() => {
        answer.value = ''
        onAnswer()
    }, 3_000)
})

onUnmounted(() => {
    clearTimeout(timer)
})
</script>

<style>
.question {
    padding-top: 2rem;
}

.question button {
    display: block;
    margin-left: auto;
}
</style>
