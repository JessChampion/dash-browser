<template>
  <div id="app">
    <Block v-bind:data="rootBlock"/>
  </div>
</template>

<script>
  import Block from './components/Block';

  export default {
    name: 'app',
    components: {
      Block,
    },
    data() {
      return {
        rootBlock: {
          id: 1,
          name: 'Block 1',
          vertical: true,
          color: null,
          children: [
            {
              id: 2,
              name: 'Block 1',
              vertical: true,
              color: 'blue',
              children: null
            }, {
              id: 3,
              name: 'Block 1',
              vertical: true,
              color: null,
              children: [{
                id: 4,
                name: 'Block 4',
                vertical: true,
                color: 'blue',
                children: null
              }, {
                id: 5,
                name: 'Block 5',
                vertical: true,
                color: 'pink',
                children: null
              }]
            }
          ]
        }
      };
    }
  };
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
