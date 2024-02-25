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
    <component :is="multi ? 'div' : 'v-radio-group'">
        <component :is="multi ? 'v-checkbox' : 'v-radio'" v-for="(item, id) in answers" :key="id" :value="item" :label="item"> </component>
    </component>
</template>
