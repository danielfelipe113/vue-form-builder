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
        {
          "label": "Label",
          "type": "select",
          "description": "a description",
          "options": [
            {
              label: "My option",
              value: 1,
              selected: true
            },
            {
              label: "My option",
              value: 1,
              selected: true
            },
          ],
          "name": "my_unique_key",
        },
        {
          "label": "Input",
          "type": "input",
          "description": "a description",
          "placeholder": "placeholder",
          "value": "",
          "name": "my_unique_key",
        },
        {
          "label": "Textarea",
          "type": "textarea",
          "description": "a description",
          "placeholder": "placeholder",
          "value": "",
          "name": "my_unique_key",
        }
      ]
    }
  }
});
</script>

<template>
  <div id="app">
    <VueDraggableFormBuilderBuilder :propAvailableElements="['input', 'select', 'textarea']" :propCurrentElements="currentElements"/>
  </div>
</template>
