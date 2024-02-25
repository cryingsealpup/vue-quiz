<script setup>
defineProps(['isEnabled']);
defineEmits(['next']);
</script>

<template>
    <v-btn variant="tonal" color="indigo-darken-3" @click="$emit('next')" :disabled="isEnabled">
        Next
    </v-btn>
</template>
