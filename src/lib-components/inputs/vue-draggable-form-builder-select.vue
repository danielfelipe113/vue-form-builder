

<template>
  
  <div class="vue-draggable-form-element">
    <label class="vue-draggable-form-element-label" :for="model.name" :class="{'block text-sm leading-5 font-medium text-gray-700': isBuilder}">{{model.label}}</label>
    <div class="vue-draggable-form-element-input-container">
      <select :id="model.name" class="vue-draggable-form-element-input" :class="{'mt-1 form-select block w-full pl-3 pr-10 py-2 text-base leading-6 border-gray-300 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 sm:text-sm sm:leading-5': isBuilder}" :disabled="disabled">
        <option v-for="(option, index) in model.options" :key="index" :value="option.value" :selected="!!option.selected">{{option.label}}</option>
      </select>
    </div>
    <p class="vue-draggable-form-element-description" :class="{'mt-2 text-sm text-gray-500': isBuilder}">{{model.description}}</p>
  </div>


</template>

<style scoped>
  
</style>

<script>
export default {
  name: 'VueDraggableFormBuilderSelect',
  data() {
    return {
      
    };
  },
  computed: {
    
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
  methods: {
    
  },
};
</script>