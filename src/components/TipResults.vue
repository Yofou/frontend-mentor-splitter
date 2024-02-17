<template>
  <div
    class="px-6 pt-[2.31rem] pb-6 md:px-10 md:pb-10 md:py-14 bg-[#00474B] rounded-[0.9375rem] flex flex-col justify-between"
  >
    <div>
      <TipAmount :amount="props.amount">Tip Amount</TipAmount>
      <TipAmount class="mt-5 md:mt-[1.56rem]" :amount="props.total">Total</TipAmount>
    </div>

    <button
      class="uppercase rounded-[.3125rem] mt-8 md:mt-0 bg-[#26C2AE] hover:bg-[#9FE8DF] py-[.5rem] font-spaceMono text-[1.25rem] text-[#00474B] font-bold transition-colors disabled:opacity-50"
      @click="onClick"
      :disabled="!canReset"
    >
      Reset
    </button>
  </div>
</template>

<script setup lang="ts">
import TipAmount from "./TipAmount.vue";

///// props/emits /////
const props = defineProps<{
  amount: number;
  total: number;
  canReset: boolean;
}>();

const emits = defineEmits<{ (e: 'reset'): void }>()

///// refs, provide or inject then variables /////

///// computed /////

///// methods /////
const onClick = () => emits('reset')

///// watchers /////

///// lifecycle /////
</script>
