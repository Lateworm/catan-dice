<template>
  <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/>
  <CatanDice msg='test'/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from './components/HelloWorld.vue';

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld,
  },
});
</script>

<style>
  /* To ensure 100% layout on mobile devices, the 100% must be applied to each child descending from html */
  html, body, body > div {
    height: 100%;
  }

  body {
    background-color: #2D2D2D;
    color: #DDDDDD;

    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

    margin: 0;
  }
</style>
