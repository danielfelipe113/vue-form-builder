

<template>
    <div class="flex flex-col  flex-1 bg-white ">
      <div class="px-4 pt-6 h-full border-gray-300" >
        
        <draggable class="min-h-full" v-model="currentElements" group="elements"  :options="{disabled: !editable}" @end="onFormChanged()">                  
          <div class="h-full py-4 px-3 mt-2 relative pt-" v-for="(elem, index) in currentElements" :key="index" :class="{' border-2 border-dashed border-gray-300': editable}">
            <div class="actionButtons flex absolute right-0" v-if="editable">
              <!-- Edit -->
              <button type="button" class="flex-shrink-0 mr-1 hover:bg-gray-200 active:bg-gray-300 transition ease-in-out duration-150 rounded" @click="editElem(elem, index)">
                <svg class="h-5 w-5"  xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                </svg>
              </button>
              <!-- Remove -->
              <button  type="button" class="flex-shrink-0 mr-1 hover:bg-gray-200 active:bg-gray-300 transition ease-in-out duration-150 rounded" @click="removeElem(elem, index)">
                <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
                </svg>
              </button>
            </div>
            <VueDraggableFormBuilderButton :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'button'" :key="index"></VueDraggableFormBuilderButton>
            <VueDraggableFormBuilderInput :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'input'" :key="index"></VueDraggableFormBuilderInput>
            <VueDraggableFormBuilderToggle :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'toggle'" :key="index"></VueDraggableFormBuilderToggle>
            <VueDraggableFormBuilderSelect :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'select'" :key="index"></VueDraggableFormBuilderSelect>
            <VueDraggableFormBuilderCheckbox :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'checkbox'" :key="index"></VueDraggableFormBuilderCheckbox>
            <VueDraggableFormBuilderRadio :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'radio'" :key="index"></VueDraggableFormBuilderRadio>
            <VueDraggableFormBuilderTextarea :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'textarea'" :key="index"></VueDraggableFormBuilderTextarea>
          </div>                
        </draggable>
      </div>
      


      <VueDraggableFormBuilderElementModalHandler :model="selectedElement" ref="elementHandlerRef" @onConfirm="onEditModalHandlerClose" v-if="editable"></VueDraggableFormBuilderElementModalHandler>
    </div>

</template>

<style>

  /* @tailwind base;
  @tailwind components;
  @tailwind utilities; */
  .actionButtons {
    top: 0.4rem;
  }

  button:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  .form-input {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    background-color: #fff;
    /* border-color: #d2d6dc;
    border-width: 1px; */
    border-radius: .375rem;
    padding: .5rem .75rem;
    font-size: 1rem;
    line-height: 1.5
}

.form-input::-webkit-input-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-input::-moz-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-input:-ms-input-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-input::-ms-input-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-input::placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-input:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(164,202,254,.45);
    border-color: #a4cafe
}

.form-textarea {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    background-color: #fff;
    border-color: #d2d6dc;
    border-width: 1px;
    border-radius: .375rem;
    padding: .5rem .75rem;
    font-size: 1rem;
    line-height: 1.5
}

.form-textarea::-webkit-input-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-textarea::-moz-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-textarea:-ms-input-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-textarea::-ms-input-placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-textarea::placeholder {
    color: #9fa6b2;
    opacity: 1
}

.form-textarea:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(164,202,254,.45);
    border-color: #a4cafe
}

.form-select {
    background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 20 20' fill='none'%3E%3Cpath d='M7 7l3-3 3 3m0 6l-3 3-3-3' stroke='%239fa6b2' stroke-width='1.5' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E");
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    -webkit-print-color-adjust: exact;
    color-adjust: exact;
    background-repeat: no-repeat;
    background-color: #fff;
    border-color: #d2d6dc;
    border-width: 1px;
    border-radius: .375rem;
    padding: .5rem 2.5rem .5rem .75rem;
    font-size: 1rem;
    line-height: 1.5;
    background-position: right .5rem center;
    background-size: 1.5em 1.5em
}

.form-select::-ms-expand {
    color: #9fa6b2;
    border: none
}

@media not print {
    .form-select::-ms-expand {
        display: none
    }
}

@media print and (-ms-high-contrast:active),print and (-ms-high-contrast:none) {
    .form-select {
        padding-right: .75rem
    }
}

.form-select:focus {
    outline: none;
    box-shadow: 0 0 0 3px rgba(164,202,254,.45);
    border-color: #a4cafe
}

.form-checkbox {
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
    -webkit-print-color-adjust: exact;
    color-adjust: exact;
    display: inline-block;
    vertical-align: middle;
    background-origin: border-box;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    flex-shrink: 0;
    height: 1rem;
    width: 1rem;
    color: #3f83f8;
    background-color: #fff;
    border-color: #d2d6dc;
    border-width: 1px;
    border-radius: .25rem
}

.form-checkbox:checked {
    background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg viewBox='0 0 16 16' fill='%23fff' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M5.707 7.293a1 1 0 00-1.414 1.414l2 2a1 1 0 001.414 0l4-4a1 1 0 00-1.414-1.414L7 8.586 5.707 7.293z'/%3E%3C/svg%3E");
    border-color: transparent;
    background-color: currentColor;
    background-size: 100% 100%;
    background-position: 50%;
    background-repeat: no-repeat
}

@media not print {
    .form-checkbox::-ms-check {
        border-width: 1px;
        color: transparent;
        background: inherit;
        border-color: inherit;
        border-radius: inherit
      }
    }

    .form-checkbox:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(164,202,254,.45);
        border-color: #a4cafe
    }

    .form-checkbox:checked:focus {
        border-color: transparent
    }

    .form-radio {
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        -webkit-print-color-adjust: exact;
        color-adjust: exact;
        display: inline-block;
        vertical-align: middle;
        background-origin: border-box;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        flex-shrink: 0;
        border-radius: 100%;
        height: 1rem;
        width: 1rem;
        color: #3f83f8;
        background-color: #fff;
        border-color: #d2d6dc;
        border-width: 1px
    }

    .form-radio:checked {
        background-image: url("data:image/svg+xml;charset=utf-8,%3Csvg viewBox='0 0 16 16' fill='%23fff' xmlns='http://www.w3.org/2000/svg'%3E%3Ccircle cx='8' cy='8' r='3'/%3E%3C/svg%3E");
        border-color: transparent;
        background-color: currentColor;
        background-size: 100% 100%;
        background-position: 50%;
        background-repeat: no-repeat
    }

    @media not print {
        .form-radio::-ms-check {
            border-width: 1px;
            color: transparent;
            background: inherit;
            border-color: inherit;
            border-radius: inherit
        }
    }

    .form-radio:focus {
        outline: none;
        box-shadow: 0 0 0 3px rgba(164,202,254,.45);
        border-color: #a4cafe
    }

    .form-radio:checked:focus {
        border-color: transparent
    }
</style>

<script>
  import draggable from 'vuedraggable';
  import VueDraggableFormBuilderButton from './inputs/vue-draggable-form-builder-button.vue';
  import VueDraggableFormBuilderInput from './inputs/vue-draggable-form-builder-input.vue';
  import VueDraggableFormBuilderToggle from './inputs/vue-draggable-form-builder-toggle.vue';
  import VueDraggableFormBuilderSelect from './inputs/vue-draggable-form-builder-select.vue';
  import VueDraggableFormBuilderRadio from './inputs/vue-draggable-form-builder-radio.vue';
  import VueDraggableFormBuilderCheckbox from './inputs/vue-draggable-form-builder-checkbox.vue';
  import VueDraggableFormBuilderTextarea from './inputs/vue-draggable-form-builder-textarea.vue';
  import VueDraggableFormBuilderElementModalHandler from './vue-draggable-form-element-modal-handler.vue';
  
  export default {
    name: 'VueDraggableFormBuilderForm',
    components: {
      draggable,
      VueDraggableFormBuilderButton,
      VueDraggableFormBuilderInput,
      VueDraggableFormBuilderToggle,
      VueDraggableFormBuilderSelect,
      VueDraggableFormBuilderCheckbox,
      VueDraggableFormBuilderRadio,
      VueDraggableFormBuilderTextarea,
      VueDraggableFormBuilderElementModalHandler
    },
    data() {
      return {
        currentElements: [],
        selectedElement: {}
      };
    },
    props: {
      editable: {
        boolean: false
      },
      propCurrentElements: {
        required: true
      }
    },
    mounted() {
      this.currentElements = this.propCurrentElements;
    },
    computed: {
      
    },
    methods: {
      editElem(elem, idx) {
        if(!!this.$refs['elementHandlerRef']) {
          this.selectedElement = elem;
          this.$refs['elementHandlerRef'].showModal();
        }
      },
      removeElem(elem, idx) {
        this.currentElements.splice(idx, 1);
        this.$forceUpdate();
      },
      onEditModalHandlerClose(elem) {
        
      },
      exportForm() {
        return [...this.currentElements];
      },
      onFormChanged() {
        this.$emit('onFormChanged');
        this.$forceUpdate();
      }
    },
  };
</script>