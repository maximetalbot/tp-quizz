<!--  -->
<template>
  <div class="container">
    <div>
      <div v-if="state === 'error'">
        Impossible de charger le quiz.
      </div>

      <div :aria-busy="state === 'loading'">
        <Quiz v-if="quiz" :quiz="quiz" />
      </div>
    </div>
  </div>

</template>



<script setup>
import { onMounted, ref } from 'vue';
import Quiz from './components/Quiz.vue';


const quiz = ref(null);
const state = ref('loading');

onMounted(async () => {
  fetch('/quiz.json')
    .then(r => {
      if (r.ok) {
        return r.json()
      } else {
        throw new Error('Impossible de récupérer le json');
      }
    })
    .then(data => {
      quiz.value = data;
      state.value = 'idle';
      console.log(quiz.value);
    })
    .catch(err => {
      state.value = 'error';
      console.error(err);
    });
});
</script>

<style>
.container {
  margin-top: 2rem;
}
</style>
