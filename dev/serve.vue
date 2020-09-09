<script>
import Vue from 'vue';
import { VueDraggableFormBuilderBuilder } from '@/entry';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueDraggableFormBuilderBuilder,
  },
  data() {
    return {
      currentElements: [
       
      ]
    }
  },
  methods: {
    onFormSave(form) {
      debugger
    }
  }
});
</script>

<template>
  <div id="app">
    <VueDraggableFormBuilderBuilder :propAvailableElements="['input', 'select', 'textarea']" :propCurrentElements="currentElements" @onFormSave="onFormSave"/>
  </div>
</template>
