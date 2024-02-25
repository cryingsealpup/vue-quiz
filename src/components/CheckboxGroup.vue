<script setup>
import { ref } from 'vue'

defineProps({
    answers: Array,
    selected: Array
})


defineEmits(['update'])

</script>

<template>
    <div class="my-4">
        <v-checkbox v-for="(item, id) in answers" @click="$emit('update', id)" :key="id" :value="item" :label="item" color="indigo-darken-3" hide-details
            density="compact">
        </v-checkbox>
    </div>
</template>
