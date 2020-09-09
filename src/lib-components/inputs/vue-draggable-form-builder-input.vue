

<template>
  
  <div class="vue-draggable-form-element">
    <label class="vue-draggable-form-element-label" :class="{'block text-sm font-medium leading-5 text-gray-700': isBuilder}" :for="model.name">{{model.label}}</label>
    <div class="vue-draggable-form-element-input-container" :class="{'mt-1 relative rounded-md shadow-sm': isBuilder}">
      <input class="vue-draggable-form-element-input" :class="{'form-input block w-full sm:text-sm sm:leading-5 border border-gray-300': isBuilder}" type="text" :id="model.name"  :placeholder="model.placeholder" :disabled="disabled" >
    </div>
    <p class="vue-draggable-form-element-description" :class="{'mt-2 text-sm text-gray-500': isBuilder}">{{model.description}}</p>
  </div>

</template>

<style scoped>
  
</style>

<script>

export default {
  components: {
    
  },
  name: 'VueDraggableFormBuilderInput',
  data() {
    return {
      
    };
  },
  props: {
    isBuilder: {
      type: Boolean,
      default: false,
    },
    model: {
      required: true
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  computed: {
    
  },
  methods: {
    
  },
};
</script>