<script setup>
import { ref, onMounted, defineProps, defineEmits } from 'vue';
import TabRenderer from './TabRenderer.vue';
import NoteSelector from './NoteSelector.vue';

const emit = defineEmits(['back', 'next']);

const props = defineProps({
  tab: {
    type: String,
    required: true,
  },
  note: {
    type: String,
    required: true,
  },
});

const getBack = () => {
  emit('back');
};

const nextExcersice = () => {
  emit('next');
};
</script>

<template>
  <div>
    <div>
      <v-btn @click="getBack">Back</v-btn>
      <v-btn @click="nextExcersice">New</v-btn>
    </div>
    <TabRenderer :tab="props.tab" />
    <NoteSelector :answerNote="props.note" />
  </div>
</template>
