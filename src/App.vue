<template>
  <div id="app">
    <Block v-bind="rootBlock"/>
  </div>
</template>

<script>
  import data from './data.json';
  import Block from './components/Block';

  export default {
    name: 'app',
    components: {
      Block,
    },
    data() {
      return {
        rootBlock: data
      };
    }
  };
</script>

<style>
  :root {
    --color-background: #EFEFEF;
    --color-black: #333333;
    --padding: 0.5rem;
    --full: 100%;
    --fullWithPadding: calc(100% - calc(var(--padding) * 2));
  }

  html, body {
    height: 100%;
    margin: 0;
  }

  #app {
    background: var(--color-background);
    color: var(--color-black);
    display: grid;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    font-size: 16px;
    min-height: var(--fullWithPadding);
    padding: var(--padding);
    width: var(--fullWithPadding);
  }
</style>
