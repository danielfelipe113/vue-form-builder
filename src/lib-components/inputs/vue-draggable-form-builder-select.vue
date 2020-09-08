

<template>
  
  <div>
    <label for="location" class="block text-sm leading-5 font-medium text-gray-700">{{model.label}}</label>
    <select id="location" class="mt-1 form-select block w-full pl-3 pr-10 py-2 text-base leading-6 border-gray-300 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 sm:text-sm sm:leading-5 " :disabled="disabled">
      <option v-for="(option, index) in model.options" :key="index" :value="option.value" :selected="!!option.selected">{{option.label}}</option>
    </select>
    <p class="mt-2 text-sm text-gray-500">{{model.description}}</p>
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