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
      currentElements:[{"label":"Selected programma","type":"select","description":"Welke workshop wenst u te volgen in de voormiddag?","options":[{"name":"","value":"1","label":"Master data management"},{"name":"","value":"2","label":"Excel Modelling"},{"name":"","value":"3","label":"KPI's die wel werken"}],"name":"selected_programma"},{"label":"Selected programma 2","type":"select","description":"Welke workshop wenst u te volgen in de namiddag?","options":[{"name":"","value":"1","label":"Efficient close process"},{"name":"","value":"2","label":"RPA"},{"name":"","value":"3","label":"Lean in Finance"}],"name":"selected_programma_2"}]
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
