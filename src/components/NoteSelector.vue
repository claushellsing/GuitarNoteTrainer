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

const chooseNote = (note) => {
  isRevealed.value = true;
};
</script>

<template>
  <div>
    <table>
      <tr>
        <td>
          <v-btn
            :color="color.do"
            :disabled="isRevealed"
            @click="chooseNote('do')"
            >DO</v-btn
          >
        </td>
      </tr>
      <tr>
        <td>
          <v-btn
            :color="color.re"
            :disabled="isRevealed"
            @click="chooseNote('re')"
            >RE</v-btn
          >
        </td>
      </tr>
      <tr>
        <td>
          <v-btn
            :color="color.mi"
            :disabled="isRevealed"
            @click="chooseNote('mi')"
            >MI</v-btn
          >
        </td>
      </tr>
      <tr>
        <td>
          <v-btn
            :color="color.fa"
            :disabled="isRevealed"
            @click="chooseNote('fa')"
            >FA</v-btn
          >
        </td>
      </tr>
      <tr>
        <td>
          <v-btn
            :color="color.sol"
            :disabled="isRevealed"
            @click="chooseNote('sol')"
            >SOL</v-btn
          >
        </td>
      </tr>
      <tr>
        <td>
          <v-btn
            :color="color.la"
            :disabled="isRevealed"
            @click="chooseNote('la')"
            >LA</v-btn
          >
        </td>
      </tr>
      <tr>
        <td>
          <v-btn
            :color="color.si"
            :disabled="isRevealed"
            @click="chooseNote('si')"
            >SI</v-btn
          >
        </td>
      </tr>
    </table>
  </div>
</template>
