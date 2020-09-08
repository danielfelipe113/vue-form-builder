

<template>
  
  <div>
    <label :for="model.name" class="block text-sm font-medium leading-5 text-gray-700">{{model.label}}</label>
    <div class="mt-1 relative rounded-md shadow-sm">
      <input type="text" :id="model.name" class="form-input block w-full sm:text-sm sm:leading-5 border border-gray-300" :placeholder="model.placeholder" :disabled="disabled">
    </div>
    <p class="mt-2 text-sm text-gray-500">{{model.description}}</p>
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