

<template>
  <div class=" pb-12">
    
    <div class="rounded-md bg-red-100 p-4 fixed top-0 w-full z-10" v-if="showGeneralErrors">
      <div class="flex">
        <div class="flex-shrink-0">
          <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
          </svg>
        </div>
        <div class="ml-3">
          <h3 class="text-sm leading-5 font-medium text-red-800" v-if="showUniqueWarning">
            Every Name key should be unique among the form
          </h3>
          <h3 class="text-sm leading-5 font-medium text-red-800" v-if="showEmptyWarning">
            Please add at least one element to the form
          </h3>
        </div>
        <button type="button" class="absolute right-0 mr-4" @click="showUniqueWarning = !showUniqueWarning">
          <svg class="h-4 w-4 text-black" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>
    </div>

    <div class=" bg-white" v-if="!!currentElements && !!availableElements">
      <h2 class="text-lg font-medium leading-6 text-gray-900 sm:truncate px-4 pt-6 uppercase">Form builder</h2>
      <div class="flex">
        <VueDraggableFormBuilderForm ref="editableForm" :propCurrentElements="currentElements" :editable="true" @onFormChanged="onFormChanged" ></VueDraggableFormBuilderForm>

        <VueFormBuilderDraggableSidebar :propAvailableElements="availableElements" @onFormChanged="onFormChanged"></VueFormBuilderDraggableSidebar>
      </div>
    </div>

    <div class="mt-5 sm:mt-6 sm:grid sm:grid-cols-2 sm:gap-3 sm:grid-flow-row-dense" style="justify-items: center;">
      <span class="flex w-full rounded-md shadow-sm sm:col-start-2 max-w-sm">
          <button type="button" class="inline-flex justify-center w-full rounded-md border border-transparent px-4 py-2 bg-indigo-600 text-base leading-6 font-medium text-white shadow-sm hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo transition ease-in-out duration-150 sm:text-sm sm:leading-5" @click="saveForm()">
              Save form
          </button>
      </span>
      <span class="mt-3 flex w-full rounded-md shadow-sm sm:mt-0 sm:col-start-1 max-w-sm">
          <button type="button" class="inline-flex justify-center w-full rounded-md border border-gray-300 px-4 py-2 bg-white text-base leading-6 font-medium text-gray-700 shadow-sm hover:text-gray-500 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue transition ease-in-out duration-150 sm:text-sm sm:leading-5 " @click="showPreviewModalFunc()" :disabled="!!this.currentElements && !this.currentElements.length">
              Preview
          </button>
      </span>
    </div>


    <div class="fixed z-10 inset-0  vue-draggable-form-preview-modal" :class="{'absolute pointer-events-none opacity-0 ease-in duration-200': !showPreviewModal, 'ease-out duration-300 opacity-100': showPreviewModal}">
      <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0" >
       
        <div class="fixed inset-0 transition-opacity" @click="closeModal">
          <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
        </div>

        <!-- This element is to trick the browser into centering the modal contents. -->
        <span class="hidden sm:inline-block sm:align-middle sm:h-screen"></span>&#8203;
        <div class="inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:p-6" role="dialog" aria-modal="true" aria-labelledby="modal-headline" style="width: 95%;" :class="{'opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95': !showPreviewModal, 'opacity-100 translate-y-0 sm:scale-100': showPreviewModal}">
          <!-- Content -->
          <VueDraggableFormBuilderForm :propCurrentElements="currentElements" v-if="showPreviewModal"></VueDraggableFormBuilderForm>
          <!-- Footer -->
          <div class="mt-5 sm:mt-6 sm:grid sm:grid-cols-2 sm:gap-3 sm:grid-flow-row-dense" style="justify-items: center;">
            <span class="flex w-full rounded-md shadow-sm sm:col-start-2 max-w-xs">
                <button type="button" class="inline-flex justify-center w-full rounded-md border border-transparent px-4 py-2 bg-indigo-600 text-base leading-6 font-medium text-white shadow-sm hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo transition ease-in-out duration-150 sm:text-sm sm:leading-5 " @click="saveForm()" >
                    Save form
                </button>
            </span>
            <span class="mt-3 flex w-full rounded-md shadow-sm sm:mt-0 sm:col-start-1 max-w-xs">
                <button type="button" class="inline-flex justify-center w-full rounded-md border border-gray-300 px-4 py-2 bg-white text-base leading-6 font-medium text-gray-700 shadow-sm hover:text-gray-500 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue transition ease-in-out duration-150 sm:text-sm sm:leading-5 " @click="closeModal()" >
                    Close
                </button>
            </span>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<style>
  

 
  
</style>

<script>
  import VueDraggableFormBuilderForm from './vue-draggable-form-form.vue';
  import VueFormBuilderDraggableSidebar from './vue-draggable-form-builder-sidebar.vue';

  export default {
    name: 'VueDraggableFormBuilderBuilder',
    components: {
      VueDraggableFormBuilderForm,
      VueFormBuilderDraggableSidebar
    },
    data() {
      return {
        showPreviewModal: false,
        showJson: false,
        showUniqueWarning: false,
        currentElements: undefined,
        availableElements: undefined,
        showGeneralErrors: false,
        showEmptyWarning: false
      };
    },
    props: {
      propAvailableElements: {
        required: true
      },
      propCurrentElements: {
        required: true
      }
    },
    mounted() {
      this.currentElements = this.propCurrentElements;
      this.checkForAvailableElements();
    },
    computed: {
     
    },
    methods: {
      closeModal() {
        this.showPreviewModal = false;
        document.body.style.overflow = 'auto';
      },
      checkForAvailableElements() {
        const availableElems = [];
        this.propAvailableElements.forEach((elem) => {
          switch(elem) {
            case 'input':
              availableElems.push({
                "label": "Input",
                "type": "input",
                "description": "a description",
                "placeholder": "placeholder",
                "value": "",
                "name": "my_unique_key",
                "required": false
              });
            break;
            case 'textarea':
              availableElems.push({
                "label": "Textarea",
                "type": "textarea",
                "description": "a description",
                "placeholder": "placeholder",
                "value": "",
                "name": "my_unique_key",
                "required": false
              });
            break;
            case 'select':
              availableElems.push({
                "label": "Select",
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
                "required": false
              });
            break;
          }
        });
        this.availableElements = availableElems;
      },
      showPreviewModalFunc() {
        this.currentElements = this.$refs['editableForm'].exportForm();
        this.$nextTick(() => {
          this.showPreviewModal = true;
          document.body.style.overflow = 'hidden';
        });
      },
      onFormChanged() {
        this.currentElements = this.$refs['editableForm'].exportForm();
        this.showUniqueWarning = false;
        this.$forceUpdate();
      },
      saveForm() {
        this.showPreviewModal = false;
        this.currentElements = this.$refs['editableForm'].exportForm();
        let uniqueKeys = true;
        if(this.currentElements.length) {
          this.currentElements.forEach((elem, idx) => {
            this.currentElements.forEach((elem2, idx2) => {
              if(idx !== idx2 && elem.name === elem2.name) {
                uniqueKeys = false;
              }
            });
          });
          if(!uniqueKeys) {
            this.showUniqueWarning = true;
            this.showGeneralErrors = true;
          } else if(!this.currentElements.length) {
            this.showEmptyWarning = true;
            this.showGeneralErrors = true;
          } else {
            this.showUniqueWarning = false;
            this.showGeneralErrors = false;
            this.$emit('onFormSave', this.currentElements);
          }
        }
      }
    },
  };
</script>