<script setup>
import NoteExercise from './NoteExercise.vue';
import NewGame from './NewGame.vue';

import { useMachine } from '@xstate/vue';
import { reactive, ref, nextTick } from 'vue';
import { createMachine, assign, interpret } from 'xstate';

const context = reactive({ data: null });
const resetExercise = ref(true);

const trainerMachine = createMachine({
  id: 'Machine Name',
  initial: 'iddle',
  states: {
    iddle: {
      on: {
        start: {
          target: 'training',
          actions: assign((_, event) => {
            return {
              currentQuestion: { ...event },
              isRevealed: false,
            };
          }),
        },
      },
    },
    training: {
      on: {
        close: {
          target: 'iddle',
        },
        next: {
          actions: assign((_, event) => {
            return {
              currentQuestion: { ...event },
            };
          }),
        },
        reveal: {},
      },
    },
  },
  context: { currentQuestion: {} },
  predictableActionArguments: true,
  preserveActionOrder: true,
});

const { state, send } = useMachine(trainerMachine);

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

const onStartSession = () => {
  const question = options[Math.floor(Math.random() * options.length)];
  send('start', {
    tab: question[0],
    note: question[1],
  });
};

const onGetBack = () => {
  send('close');
};

const onNextGame = () => {
  const question = options[Math.floor(Math.random() * options.length)];
  resetExercise.value = false;

  nextTick(() => {
    resetExercise.value = !resetExercise.value;
  });

  send('next', {
    tab: question[0],
    note: question[1],
  });
};
</script>

<template>
  <div>
    <NewGame v-if="state.matches('iddle')" @startSession="onStartSession" />

    <NoteExercise
      v-if="state.matches('training') && resetExercise"
      :tab="state.context.currentQuestion.tab"
      :note="state.context.currentQuestion.note"
      @back="onGetBack"
      @next="onNextGame"
    />
  </div>
</template>
