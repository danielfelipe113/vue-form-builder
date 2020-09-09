

<template>
  
<div class="fixed z-10 inset-0 overflow-y-auto" :class="{'absolute pointer-events-none opacity-0 ease-in duration-200': !showModal, 'ease-out duration-300 opacity-100': showModal}">
    <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
        <div class="fixed inset-0 transition-opacity">
            <div class="absolute inset-0 bg-gray-500 opacity-75"></div>
            </div>

            <!-- This element is to trick the browser into centering the modal contents. -->
            <span class="hidden sm:inline-block sm:align-middle sm:h-screen"></span>&#8203;
            <div class="inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full sm:p-6" role="dialog" aria-modal="true" aria-labelledby="modal-headline" :class="{'opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95': !showModal, 'opacity-100 translate-y-0 sm:scale-100': showModal}">
            <div>
                <div class="">
                    <h3 class="text-center text-lg leading-6 font-medium text-gray-700 mb-6" id="modal-headline">
                        Edit <span class="text-gray-900">{{ originalModel.type }}</span> field
                    </h3>
                    <div class="mt-2 mb-4">
                        <!-- name -->
                        <div class="mb-2">
                            <label for="name" class="block text-sm font-medium leading-5 text-gray-700">Name *</label>
                            <div class="mt-1 relative rounded-md shadow-sm">
                                <input type="text" id="name" class="form-input border border-gray-300 block w-full sm:text-sm sm:leading-5" placeholder="Name" v-model="originalModel.name" :class="{'border-red-300 text-red-900 placeholder-red-300 focus:shadow-outline-red focus:border-red-300': hasErrors && showNameError}" @change="validateForm">
                            </div>
                            <p class="mt-2 text-sm text-gray-500" :class="{'border-red-300 text-red-900 placeholder-red-300 focus:shadow-outline-red focus:border-red-300': hasErrors && showNameError}">An unique key per form and should not contain spaces or special characters</p>
                        </div>
                        <!-- Label -->
                        <div class="mb-2">
                            <label for="label" class="block text-sm font-medium leading-5 text-gray-700">Label *</label>
                            <div class="mt-1 relative rounded-md shadow-sm">
                                <input type="text" id="label" class="form-input border border-gray-300 block w-full sm:text-sm sm:leading-5" placeholder="Label" v-model="originalModel.label" :class="{'border-red-300 text-red-900 placeholder-red-300 focus:shadow-outline-red focus:border-red-300': hasErrors && !originalModel.label}">
                            </div>
                        </div>
                        <!-- Placeholder -->
                        <div class="mb-2" v-if="originalModel.type !== 'select'">
                            <label for="label" class="block text-sm font-medium leading-5 text-gray-700">Placeholder</label>
                            <div class="mt-1 relative rounded-md shadow-sm">
                                <input type="text" id="placeholder" class="form-input border border-gray-300 block w-full sm:text-sm sm:leading-5" placeholder="Placeholder" v-model="originalModel.placeholder">
                            </div>
                        </div>
                        <!-- Description -->
                        <div class="mb-2">
                            <label for="description" class="block text-sm font-medium leading-5 text-gray-700 mb-1">
                                Description
                            </label>
                            <div class="">
                                <div class=" flex rounded-md shadow-sm">
                                <textarea id="description" rows="3" class="form-textarea block w-full transition duration-150 ease-in-out sm:text-sm sm:leading-5" v-model="originalModel.description"></textarea>
                                </div>
                            </div>
                        </div>
                        <!-- Values -->
                        <div class="flex flex-col mb-2" v-if="originalModel.type === 'select'">
                            <h2 class="block text-sm font-medium leading-5 text-gray-700">
                                Options *
                            </h2>
                            <div class="mt-1 -my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                                <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
                                    <div class="shadow overflow-hidden border-b border-gray-300 sm:rounded-lg" >
                                        <table class="min-w-full divide-y divide-gray-200">
                                            <thead>
                                                <tr>
                                                    <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                                                        Name
                                                    </th>
                                                    <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                                                        Value
                                                    </th>
                                                    <th class="px-6 py-3 bg-gray-50 text-left text-xs leading-4 font-medium text-gray-500 uppercase tracking-wider">
                                                        
                                                    </th>
                                                </tr>
                                            </thead>
                                            <tbody>
                                                <!-- Odd row -->
                                                <tr :class="{'bg-white': idx%2 === 0, 'bg-gray-100': idx%2 !== 0}" v-for="(option, idx) in originalModel.options" :key="idx">
                                                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 font-medium text-gray-900">
                                                        {{option.label}}
                                                    </td>
                                                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500">
                                                        {{option.value}}
                                                    </td>
                                                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500 flex justify-center items-center">
                                                        <!-- Remove -->
                                                        <button  type="button" class="flex-shrink-0 mr-1 hover:bg-gray-200 active:bg-gray-300 transition ease-in-out duration-150 rounded" @click="removeOption(idx)">
                                                            <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                                                            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
                                                            </svg>
                                                        </button>
                                                    </td>
                                                </tr>

                                                <!-- Even row -->
                                                <tr class="h-20" :class="{'bg-white': originalModel.options.length%2 - 1 !== 0, 'bg-gray-100': originalModel.options.length%2 - 1 === 0}">
                                                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 font-medium text-gray-900">
                                                        <div class="mt-1 relative rounded-md shadow-sm">
                                                            <input type="text" id="optionName" class="border border-gray-300 form-input block w-full sm:text-sm sm:leading-5" placeholder="Name" v-model="newOption.label" :class="{'border-red-300 text-red-900 placeholder-red-300 focus:shadow-outline-red focus:border-red-300': hasErrors && !originalModel.options.length}">
                                                        </div>
                                                    </td>
                                                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500">
                                                        <div class="mt-1 relative rounded-md shadow-sm">
                                                            <input type="text" id="optionValue" class="form-input border border-gray-300 block w-full sm:text-sm sm:leading-5" placeholder="Value" v-model="newOption.value" :class="{'border-red-300 text-red-900 placeholder-red-300 focus:shadow-outline-red focus:border-red-300': hasErrors && !originalModel.options.length}">
                                                        </div>
                                                    </td>
                                                    <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500 flex justify-center items-center h-20">
                                                        <!-- Add -->
                                                        <button type="button" class="flex-shrink-0 mr-1 hover:bg-gray-200 active:bg-gray-300 transition ease-in-out duration-150 rounded" @click="addNewOption()">
                                                            <svg class="h-5 w-5 text-green-400" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
                                                            </svg>
                                                        </button>
                                                    </td>
                                                </tr>
                                                <!-- More rows... -->
                                            </tbody>
                                        </table>
                                    </div>
                                </div>
                            </div>
                        </div>

                    </div>
                    <!-- Errors -->
                    <div class="rounded-md bg-red-100 p-4" v-if="hasErrors && submitted">
                        <div class="flex">
                            <div class="flex-shrink-0">
                            <svg class="h-5 w-5 text-red-400" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
                            </svg>
                            </div>
                            <div class="ml-3" >
                                <h3 class="text-sm leading-5 font-medium text-red-800">
                                    There were errors with your submission
                                </h3>
                                <div class="mt-2 text-sm leading-5 text-red-700">
                                    <ul class="list-disc pl-5">
                                        <li v-if="model.type === 'select' && !model.options.length">
                                            You should have at least one option
                                        </li>
                                        <li class="mt-1" v-if="!model.name || showNameError">
                                            You must provide a name without spaces or special characters
                                        </li>
                                        <li class="mt-1" v-if="!model.label">
                                            You must provide a label
                                        </li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <!-- Footer -->
            <div class="mt-5 sm:mt-6 sm:grid sm:grid-cols-2 sm:gap-3 sm:grid-flow-row-dense">
                <span class="flex w-full rounded-md shadow-sm sm:col-start-2">
                    <button type="button" class="inline-flex justify-center w-full rounded-md border border-transparent px-4 py-2 bg-indigo-600 text-base leading-6 font-medium text-white shadow-sm hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo transition ease-in-out duration-150 sm:text-sm sm:leading-5" @click="confirmChanges()">
                        Confirm
                    </button>
                </span>
                <span class="mt-3 flex w-full rounded-md shadow-sm sm:mt-0 sm:col-start-1">
                    <button type="button" class="inline-flex justify-center w-full rounded-md border border-gray-300 px-4 py-2 bg-white text-base leading-6 font-medium text-gray-700 shadow-sm hover:text-gray-500 focus:outline-none focus:border-blue-300 focus:shadow-outline-blue transition ease-in-out duration-150 sm:text-sm sm:leading-5" @click="closeModal()">
                        Cancel
                    </button>
                </span>
            </div>
        </div>
    </div>
</div>


</template>

<style scoped>
  
</style>

<script>
class NewOption {
    constructor() {
        this.name = '';
        this.value = null;
    }
}
export default {
    name: 'VueDraggableFormBuilderElementModalHandler',
    data() {
        return {
            showModal: false,
            submitted: false,
            newOption: new NewOption(),
            hasErrors: false,
            showNameError: false,
            originalModel: {}
        }
    },
    props: {
        model: {
            required: true
        }
    },
    watch: {
        model(newVal, oldVal) {
            this.originalModel = JSON.parse(JSON.stringify(newVal));
        }
    },
    methods: {
        showModalFunc() {
            this.showModal = true;
        },
        hideModal() {
            // Reset modal on hide
            this.submitted = false;
            this.hasErrors = false;
            this.newOption = new NewOption();
            this.showModal = false;
            this.showNameError = false;
        },
        closeModal() {
            this.hideModal();
            this.$emit('onHidden');
        },
        confirmChanges() {
            this.submitted = true;
            const isValid = this.validateForm();
            if(isValid) {
                this.$emit('onConfirm', this.originalModel);
                this.hideModal();                
            } else {
                this.hasErrors = true;
            }
        },
        validateForm() {
            let isValid = true;
            if(this.originalModel.type === 'select' && !this.originalModel.options.length) {
                isValid = false;
            }
            if(!this.originalModel.label && !this.originalModel.name) {
                isValid = false;
            }
            const isKeyNameValid = this.validateKeyName();
            if(isKeyNameValid === null) {
                this.showNameError = true;
                isValid = false;
            } else {
                this.showNameError = false;
            }
            return isValid;
        },
        validateKeyName() {
            return this.originalModel.name.match(/^[a-zA-Z0-9-_]{0,}$/);
        },
        addNewOption() {
            this.originalModel.options.push(this.newOption);
            this.newOption = new NewOption();
            this.validateForm();
        },
        removeOption(idx) {
            this.originalModel.options.splice(idx, 1);
        }
    },
};
</script>