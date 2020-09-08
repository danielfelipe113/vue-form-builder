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
      availableElements: [
        {
          "label": "Label",
          "type": "select",
          "description": "a description",
          "options": [
            {
              label: "My option",
              value: 1,
              selected: true
            }
          ],
          "name": "my_unique_key",
        },
        {
          "label": "Text",
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
      ],
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
          "label": "Text",
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
    <VueDraggableFormBuilderBuilder :propAvailableItems="availableElements" :propCurrentElements="currentElements"/>
  </div>
</template>
