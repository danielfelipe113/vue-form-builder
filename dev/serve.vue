<script>
import Vue from 'vue';
import { VueDraggableFormBuilderBuilder } from '@/entry';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueDraggableFormBuilderBuilder,
  }
});
</script>

<template>
  <div id="app">
    <VueDraggableFormBuilderBuilder/>
  </div>
</template>
