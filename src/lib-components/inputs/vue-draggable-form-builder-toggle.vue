

<template>
  <div>
    <!-- On: "bg-indigo-600", Off: "bg-gray-200" -->
    <span role="checkbox" tabindex="0" aria-checked="false" class="bg-gray-200 relative inline-flex flex-shrink-0 h-6 w-11 border-2 border-transparent rounded-full cursor-pointer transition-colors ease-in-out duration-200 focus:outline-none focus:shadow-outline">
      <!-- On: "translate-x-5", Off: "translate-x-0" -->
      <span aria-hidden="true" class="translate-x-0 inline-block h-5 w-5 rounded-full bg-white shadow transform transition ease-in-out duration-200"></span>
    </span>
  </div>

  

</template>

<style scoped>
  
</style>

<script>
export default {
  name: 'VueDraggableFormBuilderToggle',
  data() {
    return {
      counter: 5,
      initCounter: 5,
      message: {
        action: null,
        amount: null,
      },
    };
  },
  computed: {
    changedBy() {
      const { message } = this;
      if (!message.action) return 'initialized';
      return `${message?.action} ${message.amount ?? ''}`.trim();
    },
  },
  methods: {
    
  },
};
</script>