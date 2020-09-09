

<template>
  <div class="hidden md:flex md:flex-shrink-0 shadow mt-8">
    <div class="flex flex-col w-64">
      <!-- Sidebar component, swap this element with another sidebar if you like -->
      <div class="flex flex-col h-0 flex-1 border-r border-gray-300 bg-gray-210">
        <div class="flex-1 flex flex-col pt-6 pb-4">
          <div class="relative flex-1 px-4 sm:px-6">
            <h2 class="text-lg font-medium leading-6 text-gray-900 sm:truncate mb-4 uppercase">Available items</h2>
            <!-- Replace with your content -->
            <draggable :list="propAvailableElements" :group="{ name: 'elements',  pull: 'clone', put: false }" :clone="clone" @end="onFormChanged()">
              <div class="h-full border-2 border-dashed border-gray-300 py-2 px-3 mb-2" v-for="(elem, index) in propAvailableElements" :key="index">
                <VueFormBuilderButton :disabled="true" :model="elem" v-if="elem.type === 'button'" :key="index"></VueFormBuilderButton>
                <VueFormBuilderInput :disabled="true" :model="elem" v-if="elem.type === 'input'" :key="index"></VueFormBuilderInput>
                <VueFormBuilderToggle :disabled="true" :model="elem" v-if="elem.type === 'toggle'" :key="index"></VueFormBuilderToggle>
                <VueFormBuilderSelect :disabled="true" :model="elem" v-if="elem.type === 'select'" :key="index"></VueFormBuilderSelect>
                <VueFormBuilderCheckbox :disabled="true" :model="elem" v-if="elem.type === 'checkbox'" :key="index"></VueFormBuilderCheckbox>
                <VueFormBuilderRadio :disabled="true" :model="elem" v-if="elem.type === 'radio'" :key="index"></VueFormBuilderRadio>
                <VueFormBuilderTextarea :disabled="true" :model="elem" v-if="elem.type === 'textarea'" :key="index"></VueFormBuilderTextarea>
              </div>                
            </draggable>
            <!-- /End replace -->
          </div>
        </div>
       
      </div>
    </div>
  </div>
 

</template>

<style scoped>
  
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
  
  export default {
    name: 'VueFormBuilderDraggableSidebar',
    components: {
      draggable,
      VueFormBuilderButton,
      VueFormBuilderInput,
      VueFormBuilderToggle,
      VueFormBuilderSelect,
      VueFormBuilderCheckbox,
      VueFormBuilderRadio,
      VueFormBuilderTextarea
    },
    data() {
      return {
        
      };
    },
    props: {
      propAvailableElements: {
        required: true
      }
    },
    mounted() {
      
    },
    computed: {
      
    },
    methods: {
      onFormChanged() {
        this.$emit('onFormChanged');
      },
      clone: function (original){
        
        
        return Object.assign({}, original);
      },
    },
  };
</script>