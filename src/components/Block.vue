<template>
  <div class="hello">
    {{name}}
  </div>
</template>

<script>
  export default {
    name: 'Block',
    props: ['data'],
    data() {
      //is leaf node
      if (this.data.children && this.data.children.length > 0) {
        return {
          isLeaf: false,
          children: this.data.children,
          vertical: true
        };
      }
      return {
        isLeaf: false,
        color: 'blue',
        vertical: true,
      };
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>
