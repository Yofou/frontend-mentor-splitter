<template>
  <fieldset>
    <slot /> 
  </fieldset>
</template>

<script setup lang="ts">
import { provide, toRef } from 'vue';

const props = defineProps<{
  disabled: boolean;
}>()

///// refs, provide or inject then variables /////
const modelValue = defineModel<number>()

const isDisabled = toRef(props, 'disabled')

provide('radio', modelValue)
provide('isDisabled', isDisabled)

///// computed /////

///// methods /////

///// watchers /////

///// lifecycle /////
</script>
