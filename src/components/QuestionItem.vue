<script setup>
import { ref } from 'vue';

defineProps({
  question: String,
  number: Number,
  total: Number
});
</script>

<template>
  <v-card class="w-100" color="indigo-darken-3" variant="tonal">
    <v-card-item>
      <div v-if="number !== total">
        <div class="text-overline mb-1">
          Question {{ number + 1 }}
        </div>
        <div class="text-h6 mb-1">
          {{ question }}
        </div>
      </div>
      <v-progress-linear :model-value="number / total * 100" color="indigo" rounded></v-progress-linear>
    </v-card-item>
  </v-card>
</template>
