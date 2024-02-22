<script setup>
import { ref, computed } from "vue";
import QuestionItem from './components/QuestionItem.vue';
import AnswersList from './components/AnswersList.vue';

import quiz from './assets/quiz.json';

const current = ref(0);
const isSelected = ref(false);
const isFinished = ref(false);
const storeAnswers = ref([]);
const currentQuestion = computed(() => {
  console.log(quiz[current.value]);
  let question = quiz[current.value];
  console.log(question);
  return question;
})

const nextQuestion = computed(() => {
  current.value < quiz.length - 1 ? current.value++ : isFinished.value = !isFinished.value;
  return current.value < quiz.value.length;
})

</script>

<template>
  <h1>The Quiz</h1>

  <div>
    <QuestionItem :question="currentQuestion.question" />
    <v-divider></v-divider>
    <AnswersList :answers="currentQuestion.answers" :multi="currentQuestion.multi" />
  </div>
  <button @click="nextQuestion"> Next </button>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
