

<template>
  
  <div class="vue-draggable-form-element">
    <label class="vue-draggable-form-element-label" :for="model.name" :class="{'block text-sm font-medium leading-5 text-gray-700': isBuilder}">{{model.label}} <span v-if="model.required">&nbsp;*</span></label>
    <div class="vue-draggable-form-element-input-container" :class="{'mt-1 relative rounded-md shadow-sm': isBuilder}">
      <textarea class="vue-draggable-form-element-input" :id="model.name" rows="3" :class="{'form-textarea block w-full transition duration-150 ease-in-out sm:text-sm sm:leading-5 border border-gray-300': isBuilder}" :placeholder="model.placeholder" :disabled="disabled"  :required="model.required"></textarea>
    </div>
    <p class="vue-draggable-form-element-description" :class="{'mt-2 text-sm text-gray-500': isBuilder}">{{model.description}}</p>
  </div>

</template>

<style scoped>
  
</style>

<script>
export default {
  name: 'VueDraggableFormBuilderTextarea',
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