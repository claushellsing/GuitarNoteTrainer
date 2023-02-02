<script setup>
import { ref, onMounted, defineProps } from 'vue';
import TabRenderer from './TabRenderer.vue';
import NoteSelector from './NoteSelector.vue';

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
</script>

<template>
  <div>
    <TabRenderer :tab="props.tab" />
    <NoteSelector :answerNote="props.note" />
  </div>
</template>
