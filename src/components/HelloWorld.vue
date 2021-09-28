<template>
  <main>
    <div class='title-container' v-if='state.roll[0] === 0'>
      <h2>Catan Dice</h2>
    </div>

    <div class='dice-container' v-else>
      <p>Roll {{ state.rolls }}</p>
      <h1 v-bind:class='{ seven: state.roll[0] + state.roll[1] === 7 }' v-cloak>{{ state.roll[0] + state.roll[1] }}</h1>

      <div class='dice'>
        <div class='die'><span>{{ state.roll[0] }}</span></div>
        <div class='die'><span>{{ state.roll[1] }}</span></div>
      </div>
    </div>

    <div class='button-container'>
      <button v-on:click='draw()'>
        <span>Roll the bones!</span>
      </button>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String,
  },

  setup () {
    type State = {
      die: number[];
      deck: number[][];
      roll: number[];
      rolls: number;
    };

    const state: State = reactive({
      die: [1, 2, 3, 4, 5, 6],
      deck: [],
      roll: [0, 0],
      rolls: 0,
    });

    const buildDeck = () => {
      state.die.forEach(roll1 => {
        state.die.forEach(roll2 => {
          state.deck.push([roll1, roll2]);
        });
      });
    };

    const draw = () => {
      state.roll = state.deck.splice((Math.floor(Math.random() * state.deck.length)), 1)[0];
      state.rolls++;
      if (state.deck.length === 0) {buildDeck();}
    };

    buildDeck();

    return {
      state,
      draw,
    };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  [v-cloak] {display: none}

  /* GRID LAYOUT */

  main {
    width: 100%;
    height: 100%;
    /* max-height: -webkit-fill-available; */

    display: grid;
    grid-template-columns: auto 20rem auto;
    grid-template-rows: auto 15rem auto auto;
  }

  .title-container {
    grid-column-start: 2;
    grid-column-end: 3;
    grid-row-start: 2;
    grid-row-end: 3;

    display: flex;
    align-items: center;
    justify-content: center;
  }

  .dice-container {
    grid-column-start: 2;
    grid-column-end: 3;
    grid-row-start: 2;
    grid-row-end: 3;

    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }

  .button-container {
    grid-column-start: 2;
    grid-column-end: 3;
    grid-row-start: 3;
    grid-row-end: 4;

    display: flex;
    align-items: center;
    justify-content: center;
  }

  /* ELEMENTS */

  button {
    background-color: #579AD1;
    color: #FFFFFF;
    border: 0px;
    border-radius: 2px;

    padding: 1rem;
    font-size: 1.5rem;
  }

  h1 {
    font-size: 8rem;
    margin: 0 0 1rem 0;
  }

  h2 {
    font-size: 6rem;
    text-align: center;
    color: #8ACE94;
  }

  .dice {
    display: flex;
  }

  .die {
    background-color: #8ACE94;
    color: #252526;
    border-radius: 2px;
    font-size: 1.5rem;
    width: 2rem;
    height: 2rem;

    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    text-align: center;
  }

  .die:nth-child(1) {
    margin-right: 0.5rem;
  }

  .seven {
    color: #FF6E76;
  }
</style>
