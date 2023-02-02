<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['start-session']);

const startSession = () => {
  emit('start-session');
};
</script>

<template>
  <div>
    <v-btn @click="startSession">New Session</v-btn>
  </div>
</template>
