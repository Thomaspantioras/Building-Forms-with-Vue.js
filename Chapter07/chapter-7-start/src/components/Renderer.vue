<template>
        <component 
          :is="component" 
          v-bind="props"
          :value="value"
          @input="handleComponentInput"
        />
      </template>
      <script>
export default {
  props: {
    element: {
      type: Object,
      required: true
    },
    value: {
      required: true
    }
  },
  computed: {
    component() {
      const componentName = this.element.component;
      return () => import(`./${componentName}`);
    },
    /* 
    will simply pass down the whole element with its properties as props 
    to whatever component we are loading using the v-on binding. If you are wondering 
    why we are using a computed property instead of just passing the element directly 
    to the v-on directive, it is because allows us to, later on, add another level of 
    logic or parsing that could be needed for a particular component.
    */
    props() {
      return this.element;
    }
  },
  methods: {
    handleComponentInput(value) {
      this.$emit("input", value);
    }
  }
};
</script>