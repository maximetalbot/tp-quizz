<template>
    <div>
        Etape {{ value + 1 }} sur {{ max + 1 }}
    </div>
    <progress :value="value" :max="max"/>
</template>

<script setup>
defineProps({
    value: Number,
    max: Number
})
</script>

<style scoped></style>
