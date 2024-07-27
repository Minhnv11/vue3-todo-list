<script setup>

import {defineEmits, defineProps} from 'vue';

const props = defineProps({
    tabs: {
        type: Array,
        required: true,
    },
    selectedTab: {
        type : String,
        required: true,
    },
});

const emit = defineEmits(['select-tab']);

const selectTab = (tab) => {
    emit('select-tab', tab);
}
</script>

<template>
    <div>
        <!-- Tabs navs -->
        <button v-for="tab in tabs" :key="tab.id" 
        :class="{ active: tab.name === selectedTab }"
        @click="selectTab(tab.name)"
        class="btn btn-outline-secondary m-2"> {{ tab.name }}</button>
       
        <!-- Tabs navs -->
    </div>

</template>

<style scoped></style>
