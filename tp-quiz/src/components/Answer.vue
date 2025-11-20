<template>
    <label :for="id" :class="classes">
        <input :disabled="disabled" type="radio" name="answer" :id="id" :value="value" @change="onChange" />
        {{ value }}
    </label>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
    id: String,
    disabled: Boolean,
    value: String,
    correctAnswer: String
})
const emits = defineEmits(['change'])
const model = defineModel()
const classes = computed(() => ({
    right: props.disabled && props.value === props.correctAnswer,
    wrong: props.disabled && props.value !== props.correctAnswer,
    disabled: props.disabled
}))
const onChange = () => {
    emits('change', props.value)
    model.value = props.value
}

</script>

<style>
.disabled {
    opacity: .5;
}

.right {
    color: green;
    opacity: 1
}

.wrong {
    color: red;
    opacity: .5
}
</style>