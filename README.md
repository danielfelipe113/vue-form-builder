# Dependencies

## Vue
[https://vuejs.org](https://vuejs.org/ "Vuejs")

## Vue.Draggable
[https://github.com/SortableJS/Vue.Draggable](https://github.com/SortableJS/Vue.Draggable "Vue.Draggable")

## Tailwind
[https://tailwindcss.com/](https://tailwindcss.com/ "Tailwind")

# Get started
```javascript
import { VueDraggableFormBuilderBuilder } from 'vue-draggable-form-builder';

...
components: {
    VueDraggableFormBuilderBuilder
},

...
<VueDraggableFormBuilderBuilder
    :propAvailableElements="['input', 'select', 'textarea']"
    :propCurrentElements="currentElements"
/>
```

### propAvailableElements
> Array with any of input, select, textarea items

### propCurrentElements [TODO: change name]
> An existing representation of the items
```
[
    {
        "label": "Textarea",
        "type": "textarea",
        "description": "a description",
        "placeholder": "placeholder",
        "value": "",
        "name": "my_unique_key"
    },
    {
        "label": "Label",
        "type": "select",
        "description": "a description",
        "options": [
        {
            "label": "My option",
            "value": 1,
            "selected": true
        },
        {
            "label": "My option",
            "value": 1,
            "selected": true
        }
        ],
        "name": "my_unique_key2"
    },
    {
        "label": "Input",
        "type": "input",
        "description": "a description",
        "placeholder": "placeholder",
        "value": "",
        "name": "my_unique_key3"
    }
]
```

# Rendering the form
```javascript
<VueDraggableFormBuilderBuilder
    :propCurrentElements="currentElements"
/>
```


