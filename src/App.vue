<script setup>
import { ref, computed } from "vue";

import QuestionItem from './components/QuestionItem.vue';
import CheckboxGroup from "./components/CheckboxGroup.vue";
import RadioGroup from "./components/RadioGroup.vue";
import NextButton from "./components/NextButton.vue";
import ResultsBox from './components/ResultsBox.vue';

import quiz from './assets/quiz.json';

const current = ref(0);
const isFinished = ref(false);
const isDisabled = ref(true);
const storeAnswers = ref(Array.from({ length: quiz.length }, (el) => []));
const currentQuestion = computed(() => quiz[current.value]);

const nextQuestion = () => {
  current.value < quiz.length - 1 ? current.value++ : isFinished.value = !isFinished.value;
}

const addAnswer = (answer) => {
  if (storeAnswers.value[current.value].length < 2 && answer === storeAnswers.value[current.value].slice(-1)[0]) {
    isDisabled.value = true;
    return;
  } 
  
  if (storeAnswers.value[current.value].indexOf(answer) !== -1) {
    storeAnswers.value[current.value].splice(storeAnswers.value[current.value].indexOf(answer), 1);
    return;
  }
  currentQuestion.value.multi ? storeAnswers.value[current.value].push(answer) : storeAnswers.value[current.value] = [answer];
  isDisabled.value = false;

  console.log(storeAnswers.value)
}

const validateAnswers = computed(() => storeAnswers.value.map((el, index) => {
  const temp = {
    question: quiz[index].question,
    correctAnswers: quiz[index].correctAnswer.map((answer) => quiz[index].answers[answer]),
    userAnswers: [...el].map((answer) => quiz[index].answers[answer]),
  }

  temp['isCorrectlyGuessed'] = temp['correctAnswers'].every((answer) => temp['userAnswers'].includes(answer)) && temp['userAnswers'].length === temp['correctAnswers'].length;
  return temp;
}));
</script>

<template>
  <div class="ma-auto w-50 my-8">
    <div>
      <QuestionItem :question="currentQuestion.question" :number="isFinished ? current + 1 : current"
        :total="quiz.length" />
      <CheckboxGroup :answers="currentQuestion.answers" @update="addAnswer" :key="current"
        v-if="currentQuestion.multi && !isFinished" />
      <RadioGroup :answers="currentQuestion.answers" @update="addAnswer" :key="current + 1" v-else-if="!isFinished" />
    </div>
    <NextButton @next="nextQuestion" v-if="!isFinished" :isEnabled="isDisabled" />
    <ResultsBox :results="validateAnswers" v-else />
  </div>
</template>