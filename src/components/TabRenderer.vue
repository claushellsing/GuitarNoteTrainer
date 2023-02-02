<script setup>
import { ref, defineProps } from 'vue';
import styles from '../assets/css/chordictionary.css';

import * as chordictionary from 'chordictionary';

const props = defineProps({
  tab: {
    type: String,
    required: true,
  },
});

const chordHtml = ref('');
let myInstrument = new chordictionary.Instrument('EADGBE', 19, 4, 4);
chordHtml.value = myInstrument.getChordLayout(props.tab, {
  name: ' ',
});
</script>

<template>
  <div v-html="chordHtml"></div>
</template>
