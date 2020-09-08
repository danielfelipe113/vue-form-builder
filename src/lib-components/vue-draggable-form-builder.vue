

<template>
  <div class=" pb-12">
    
    <div class="rounded-md bg-red-100 p-4 fixed top-0 w-full z-10" v-if="showUniqueWarning">
      <div class="flex">
        <div class="flex-shrink-0">
          <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
          </svg>
        </div>
        <div class="ml-3">
          <h3 class="text-sm leading-5 font-medium text-red-800">
            Every Name key should be unique among the form
          </h3>
        </div>
      </div>
    </div>

    <div class=" flex bg-white" v-if="!!currentElements">
      <VueDraggableFormBuilderForm ref="editableForm" :propCurrentElements="currentElements" :editable="true" @onFormChanged="onFormChanged" ></VueDraggableFormBuilderForm>

      <VueFormBuilderDraggableSidebar :propAvailableItems="propAvailableItems" @onFormChanged="onFormChanged"></VueFormBuilderDraggableSidebar>
    </div>

    <div class="mt-5 sm:mt-6 sm:grid sm:grid-cols-2 sm:gap-3 sm:grid-flow-row-dense justify-items-center">
      <span class="flex w-full rounded-md shadow-sm sm:col-start-2 max-w-sm">
          <button type="button" class="inline-flex justify-center w-full rounded-md border border-transparent px-4 py-2 bg-indigo-600 text-base leading-6 font-medium text-white shadow-sm hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo transition ease-in-out duration-150 sm:text-sm sm:leading-5" @click="saveForm()" :disabled="!this.currentElements.length">
              Save form
          </button>
      </span>
      <span class="mt-3 flex w-full rounded-md shadow-sm sm:mt-0 sm:col-start-1 max-w-sm">
          <button type="button" class="inline-flex justify-center w-full rounded-md border border-gray-300 px-4 py-2 bg-white text-base leading-6 font-medium text-gray-700 shadow-sm hover:text-gray-500 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue transition ease-in-out duration-150 sm:text-sm sm:leading-5 " @click="showPreviewModalFunc()" :disabled="!this.currentElements.length">
              Preview
          </button>
      </span>
    </div>


    <div class="fixed z-10 inset-0 overflow-y-auto" :class="{'absolute pointer-events-none opacity-0 ease-in duration-200': !showPreviewModal, 'ease-out duration-300 opacity-100': showPreviewModal}">
      <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0" >
       
        <div class="fixed inset-0 transition-opacity" @click="closeModal">
          <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
        </div>

        <!-- This element is to trick the browser into centering the modal contents. -->
        <span class="hidden sm:inline-block sm:align-middle sm:h-screen"></span>&#8203;
        
        <div class="inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:p-6" role="dialog" aria-modal="true" aria-labelledby="modal-headline" style="width: 95%;" :class="{'opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95': !showPreviewModal, 'opacity-100 translate-y-0 sm:scale-100': showPreviewModal}">
          <!-- Content -->
          <VueDraggableFormBuilderForm :propCurrentElements="currentElements" ></VueDraggableFormBuilderForm>
          <!-- Footer -->
          <div class="mt-5 sm:mt-6 sm:grid sm:grid-cols-2 sm:gap-3 sm:grid-flow-row-dense justify-items-center">
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
    <pre v-if="showJson">
      {{
        currentElements
      }}

    </pre>
  </div>

</template>

<style>

  button:disabled {
    @apply opacity-50 cursor-not-allowed;
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
        currentElements: undefined
      };
    },
    props: {
      propAvailableItems: {
        required: true
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
      closeModal() {
        this.showPreviewModal = false;
      },
      showPreviewModalFunc() {
        this.currentElements = this.$refs['editableForm'].exportForm();
        this.showPreviewModal = true;
      },
      onFormChanged() {
        this.currentElements = this.$refs['editableForm'].exportForm();
        this.showUniqueWarning = false;
      },
      saveForm() {
        this.showPreviewModal = false;
        this.currentElements = this.$refs['editableForm'].exportForm();
        let uniqueKeys = true;
        if(this.currentElements.length) {
          this.currentElements.forEach((elem) => {
            this.currentElements.forEach(elem2 => {
              if(elem.name === elem2.name) {
                uniqueKeys = false;
              }
            });
          });
          if(!uniqueKeys) {
            this.showUniqueWarning = true;
          } else {
            this.showJson = true;
          }
        }
      }
    },
  };
</script>