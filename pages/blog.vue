<!--  -->
<template>
  <h1>Blog</h1>
  <pre>
    {{ data }}
  </pre>
</template>

<script setup>
const {data} = useFetch('https://jsonplaceholder.typicode.com/posts')
console.log(data)
</script>