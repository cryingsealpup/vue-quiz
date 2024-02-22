<script setup>
import { ref } from 'vue'

defineProps({
    answers: Array,
    multi: Boolean
})

const count = ref(0)
</script>

<template>
    {{ multi }}
    <div>
        <v-radio :is="multi ? 'v-checkbox' : 'v-radio'" v-for="(item, id) in answers" :key="id" :value="item">  {{ item }} </v-radio>
    </div>
</template>
