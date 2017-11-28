<template>
  <div v-if="leaf" :class="classes" :id="`block-${id}`">
    {{id}} : {{url}}
  </div>
  <div v-else :class="classes">
    <Block v-bind="getChild(0)"/>
    <Block v-bind="getChild(1)"/>
  </div>
</template>

<script>
  const getClasses = (leaf, vertical) => {
    if (leaf) {
      return 'block leaf';
    }
    return `block ${vertical ? 'vertical' : 'horizontal'} `;
  };

  const isLeafNode = children => !children || children.length === 0;

  export default {
    name: 'Block',
    props: {
      id: Number,
      url: String,
      size: Number,
      vertical: Boolean,
      children: Array
    },
    methods: {
      resize: (percentage) => {
        // eslint-disable-next-line no-console
        console.log(`resize ${percentage}`);
      },
      setUrl: (url) => {
        // eslint-disable-next-line no-console
        console.log(`setUrl ${url}`);
      },
      split: () => {
        // eslint-disable-next-line no-console
        console.log('split');
      }
    },
    data() {
      const leaf = isLeafNode(this.children);
      return {
        classes: getClasses(this.leaf, this.vertical),
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
    border: var(--borderWidth) solid var(--color-black);
    width: 100%;
    height: 100%;
    min-height: 100%;
  }

  .block.vertical {
    grid-template-columns: 50% 50%;
    grid-template-rows: 100%;
  }

  .block.horizontal {
    grid-template-columns: 100%;
    grid-template-rows: 50% 50%;
  }

  .leaf {
    display: block;
  }
</style>
