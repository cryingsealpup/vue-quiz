<script setup>
import { ref } from 'vue';
defineProps({
    results: Array
})
</script>

<template>
    <div class="d-flex align-center flex-column my-auto mt-5">
        <div class="text-h6 ml-n3">
            Your score is
        </div>
        <div class="text-h2">
            {{ results.reduce((acc, el) => el.isCorrectlyGuessed ? acc + 1 : acc, 0) }}
            <span class="text-h6 ml-n3">/{{ results.length }}</span>
        </div>
    </div>
    <v-alert variant="outlined" class="my-4" v-for="(result, key) in results" :key="key"
        :type="result.isCorrectlyGuessed ? 'success' : 'error'">
        <v-alert-title>
            {{ result.question }}
        </v-alert-title>

        <v-alert-text>
            <div class="my-2" v-if="!result.isCorrectlyGuessed">
                <p class="font-weight-black">Correct {{ result.correctAnswers.length > 1 ? 'Answers' : 'Answer' }}:</p>
                <p v-for="answer in result.correctAnswers"> <v-icon icon="mdi-circle-small"></v-icon> {{ answer }} </p>
            </div>
            <div class="my-2">
                <p class="font-weight-black">Your {{ result.correctAnswers.length > 1 ? 'Answers' : 'Answer' }}:</p>
                <p v-for="answer in result.userAnswers"> <v-icon icon="mdi-circle-small"></v-icon> {{ answer }} </p>
            </div>
        </v-alert-text>
    </v-alert>
</template>
