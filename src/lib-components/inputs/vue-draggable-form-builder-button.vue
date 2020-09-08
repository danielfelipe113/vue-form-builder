

<template>
  
  <span class="inline-flex rounded-md shadow-sm">
    <button type="button" class="inline-flex items-center px-6 py-3 border border-transparent text-base leading-6 font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo active:bg-indigo-700 transition ease-in-out duration-150">
      <svg class="-ml-1 mr-3 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path d="M2.003 5.884L10 9.882l7.997-3.998A2 2 0 0016 4H4a2 2 0 00-1.997 1.884z" />
        <path d="M18 8.118l-8 4-8-4V14a2 2 0 002 2h12a2 2 0 002-2V8.118z" />
      </svg>
      Button text
    </button>
  </span>
  

</template>

<style scoped>
  
</style>

<script>
export default {
  name: 'VueDraggableFormBuilderButton',
  data() {
    return {
     
    };
  },
  computed: {
    
  },
  props: {
    disable: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    
  },
};
</script>