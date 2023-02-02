<script setup>
import NoteExercise from './NoteExercise.vue';

const options = [
  // 1
  ['XXXXX0', 'mi'],
  ['XXXXX1', 'fa'],
  ['XXXXX3', 'sol'],
  // 2
  ['XXXX0X', 'si'],
  ['XXXX1X', 'do'],
  ['XXXX3X', 're'],
  // 3
  ['XXX0XX', 'sol'],
  ['XXX2XX', 'la'],
  // 4
  ['XX0XXX', 're'],
  ['XX2XXX', 'mi'],
  ['XX3XXX', 'fa'],
  // 5
  ['X0XXXX', 'la'],
  ['X2XXXX', 'si'],
  ['X3XXXX', 'do'],
  // 6
  ['0XXXXX', 'mi'],
  ['1XXXXX', 'fa'],
  ['3XXXXX', 'sol'],
];

const excercise = options[16];
</script>

<template>
  <div>
    <NoteExercise :tab="excercise[0]" :note="excercise[1]" />
  </div>
</template>
