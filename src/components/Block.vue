<template>
  <div v-if="leaf"
       :id="`block-${id}`"
       :class="classes"
       :style="styles"
  >
    {{content.url}}
  </div>
  <div v-else
       :class="classes"
       :style="styles"
  >
    <Block v-bind="children[0]"/>
    <Block v-bind="children[1]"/>
  </div>
</template>

<script>
  const isLeafNode = children => !children || children.length === 0;

  const getOrientation = vertical => (vertical ? 'vertical' : 'horizontal');

  // todo: impliment resizing
  //  const getResizeStyles = orientation => `resize: ${orientation}`;

  const getGridStyles = (children, vertical) => {
    const childSizes = children.map(x => x.size);

    if (vertical) {
      return `grid-template-columns: ${childSizes[0]}% ${childSizes[1]}%;`;
    }
    return `grid-template-rows: ${childSizes[0]}% ${childSizes[1]}%;`;
  };

  const getClasses = (leaf, orientation) => {
    if (leaf) {
      return 'block leaf';
    }
    return `block ${orientation}`;
  };


  export default {
    name: 'Block',
    props: {
      id: Number,
      content: { url: String },
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
      const orientation = getOrientation(this.vertical);
      const classes = getClasses(this.leaf, orientation);
      const styles = leaf ? '' : getGridStyles(this.children, this.vertical);

      return {
        classes,
        leaf,
        orientation,
        styles
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

  .leaf {
    display: block;
    overflow: auto;
  }
</style>
