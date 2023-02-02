<script setup>
import { ref, defineProps, computed } from 'vue';

const props = defineProps({
  answerNote: {
    type: String,
    required: true,
  },
});

const notes = ['do', 're', 'mi', 'fa', 'sol', 'la', 'si'];
const responses = notes.map((note) => [
  note,
  note === props.answerNote ? 'green' : 'error',
]);

const isRevealed = ref(false);

const color = computed(() => {
  if (isRevealed.value) {
    return Object.fromEntries(responses);
  }
  return '';
});

const shuffledNotes = computed(() => {
  return [...notes].sort(function () {
    return Math.random() - 0.5;
  });
});

const chooseNote = (note) => {
  isRevealed.value = true;
};
</script>

<template>
  <div>
    <table>
      <tr :key="index" v-for="(note, index) in shuffledNotes">
        <td>
          <v-btn
            :color="color[note]"
            :disabled="isRevealed"
            @click="chooseNote(note)"
            >{{ note.toUpperCase() }}</v-btn
          >
        </td>
      </tr>
    </table>
  </div>
</template>
