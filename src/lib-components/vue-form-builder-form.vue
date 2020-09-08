

<template>
    <div class="flex flex-col  flex-1 bg-white ">
      <div class="px-4 pt-6 h-full border-gray-300" >
        <h2 class="text-lg font-medium leading-6 text-gray-900 sm:truncate mb-4 uppercase">Form builder</h2>
        <draggable v-model="currentElements" group="elements" class="" :options="{disabled: !editable}" @end="onFormChanged()">                  
          <div class="h-full py-4 px-3 mt-2 relative pt-" v-for="(elem, index) in currentElements" :key="index" :class="{' border-2 border-dashed border-gray-300': editable}">
            <div class="actionButtons flex absolute right-0" v-if="editable">
              <!-- Edit -->
              <button class="flex-shrink-0 mr-1 hover:bg-gray-200 active:bg-gray-300 transition ease-in-out duration-150 rounded" @click="editElem(elem, index)">
                <svg class="h-5 w-5"  xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z" />
                </svg>
              </button>
              <!-- Remove -->
              <button class="flex-shrink-0 mr-1 hover:bg-gray-200 active:bg-gray-300 transition ease-in-out duration-150 rounded" @click="removeElem(elem, index)">
                <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
                </svg>
              </button>
            </div>
            <VueFormBuilderButton :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'button'" :key="index"></VueFormBuilderButton>
            <VueFormBuilderInput :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'input'" :key="index"></VueFormBuilderInput>
            <VueFormBuilderToggle :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'toggle'" :key="index"></VueFormBuilderToggle>
            <VueFormBuilderSelect :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'select'" :key="index"></VueFormBuilderSelect>
            <VueFormBuilderCheckbox :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'checkbox'" :key="index"></VueFormBuilderCheckbox>
            <VueFormBuilderRadio :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'radio'" :key="index"></VueFormBuilderRadio>
            <VueFormBuilderTextarea :disabled="editable" :ref="'elemRef' + index" :model="elem" v-if="elem.type === 'textarea'" :key="index"></VueFormBuilderTextarea>
          </div>                
        </draggable>
      </div>
      


      <VueFormBuilderElementModalHandler :model="selectedElement" ref="elementHandlerRef" @onConfirm="onEditModalHandlerClose" v-if="editable"></VueFormBuilderElementModalHandler>
    </div>

</template>

<style scoped>
  .actionButtons {
    top: 0.4rem;
  }
</style>

<script>
  import draggable from 'vuedraggable';
  import VueFormBuilderButton from './inputs/vue-draggable-form-builder-button.vue';
  import VueFormBuilderInput from './inputs/vue-draggable-form-builder-input.vue';
  import VueFormBuilderToggle from './inputs/vue-draggable-form-builder-toggle.vue';
  import VueFormBuilderSelect from './inputs/vue-draggable-form-builder-select.vue';
  import VueFormBuilderRadio from './inputs/vue-draggable-form-builder-radio.vue';
  import VueFormBuilderCheckbox from './inputs/vue-draggable-form-builder-checkbox.vue';
  import VueFormBuilderTextarea from './inputs/vue-draggable-form-builder-textarea.vue';
  import VueFormBuilderElementModalHandler from './vue-draggable-form-builder-element-modal-handler.vue';
  
  export default {
    name: 'VueFormBuilderForm',
    components: {
      draggable,
      VueFormBuilderButton,
      VueFormBuilderInput,
      VueFormBuilderToggle,
      VueFormBuilderSelect,
      VueFormBuilderCheckbox,
      VueFormBuilderRadio,
      VueFormBuilderTextarea,
      VueFormBuilderElementModalHandler
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
      },
      onEditModalHandlerClose(elem) {
        
      },
      exportForm() {
        return [...this.currentElements];
      },
      onFormChanged() {
        this.$emit('onFormChanged');
      }
    },
  };
</script>