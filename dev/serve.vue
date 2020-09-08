<script>
import Vue from 'vue';
import { VueFormBuilderBuilder } from '@/entry';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueFormBuilderBuilder,
  }
});
</script>

<template>
  <div id="app">
    <vue-form-builder-builder />
  </div>
</template>
