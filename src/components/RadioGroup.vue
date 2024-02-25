<script setup>
import { ref } from 'vue';
defineProps({
    answers: Array
})

const emits = defineEmits(['update']);
const currentValue = ref(null);
</script>

<template>
    <v-radio-group density="compact" class="mt-4" v-model="currentValue" @update:modelValue="$emit('update', currentValue)">
        <v-radio v-for="(item, key) in answers" :key="key" :value="key" :label="item" color="indigo-darken-3"></v-radio>
    </v-radio-group>
</template>
