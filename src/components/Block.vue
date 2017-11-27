<template>
  <div v-if="leaf" :class="classes">
    {{id}} : {{name}}
  </div>
  <div v-else :class="classes">
    <Block v-bind="getChild(0)"/>
    <Block v-bind="getChild(1)"/>
  </div>
</template>

<script>
  const getClasses = (leaf, color, vertical) => {
    if (leaf) {
      return `block leaf color-${color}`;
    }
    const orientation = vertical ? 'vertical' : 'horizontal';
    return `block ${orientation}`;
  };

  const isLeafNode = children => !children || children.length === 0;

  export default {
    name: 'Block',
    props: {
      id: Number,
      name: String,
      vertical: Boolean,
      color: String,
      children: Array
    },
    data() {
      const leaf = isLeafNode(this.children);
      return {
        classes: getClasses(this.leaf, this.color, this.vertical),
        leaf,
        getChild: (index) => {
          if (leaf || index === 0 || index === 1) {
            return this.children[index];
          }
          return null;
        }
      };
    }
  };
</script>

<style>
  .block {
    display: grid;
    border: 1px solid var(--color-black);
    width: 100%;
    height: 100%;
    min-height: 100%;
  }

  .block.vertical{
    grid-template-columns: 50% 50%;
    grid-template-rows: 100%;
  }

  .block.horizontal{
    grid-template-columns: 100%;
    grid-template-rows: 50% 50%;
  }

  .leaf{
    display: block;
  }

</style>
