<template>
  <main class="w-full min-h-screen grid grid-rows-[max-content,1fr] md:grid-rows-[max-content,max-content] items-end justify-items-center md:items-start pt-[3.12rem] md:pt-[10.19rem] md:pb-12 bg-[#C5E4E7]">
    <SplitterIcon />
    <TipCard class="grid grid-cols-1 md:grid-cols-[1fr,minmax(0,25.8125rem)] gap-8 md:gap-12 mt-[2.55rem] md:mt-[5.49rem]">
      <TipForm
        v-model:bill="bill"
        v-model:numberOfPeople="numberOfPeople"
        v-model:tipPerct="tipPerct"
      />
      <TipResults 
        :amount="tip" 
        :total="total"
        :canReset="canReset"
        @reset="onReset" 
      />
    </TipCard>
  </main>
</template>

<script setup lang="ts">
import TipCard from "./components/TipCard.vue";
import TipResults from "./components/TipResults.vue";
import TipForm from "./components/TipForm.vue";
import SplitterIcon from './components/Icons/Splitter.vue'
import "@fontsource/space-mono/400.css";
import "@fontsource/space-mono/700.css";
import { computed, ref } from "vue";

const bill = ref(0);
const numberOfPeople = ref(1);
const tipPerct = ref<number>();

const tip = computed(() => {
  if (numberOfPeople.value == 0) {
    return 0;
  }

  return (bill.value * (tipPerct.value ?? 0)) / numberOfPeople.value;
});

const total = computed(() => {
  if (numberOfPeople.value == 0) {
    return 0;
  }
  
  return (bill.value / numberOfPeople.value) + tip.value;
});

const canReset = computed(() => {
  return bill.value != 0 || numberOfPeople.value != 1 || tipPerct.value != null;
})

const onReset = () => {
  bill.value = 0;
  numberOfPeople.value = 1;
  tipPerct.value = undefined;
};
</script>
