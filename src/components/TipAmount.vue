<template>
  <div class="flex justify-between gap-4 items-center flex-shrink-0">
    <div class="flex-shrink-0">
      <p class="text-[1rem] font-spaceMono font-bold text-white"><slot /></p>
      <p class="text-[0.8125rem] font-spaceMono font-bold text-[#7F9D9F]">
        / person
      </p>
    </div>

    <h2
      class="text-[#26C2AE] text-[2rem] md:text-[3rem] font-spaceMono font-bold tracking-[-0.04169rem] md:tracking-[-0.0625rem] truncate"
    >
      {{ amount }}
    </h2>
  </div>
</template>

<script setup lang="ts">
import { computed } from "vue";
///// props/emits /////
const props = defineProps<{ amount: number }>();

const formatter = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",

  // These options are needed to round to whole numbers if that's what you want.
  //minimumFractionDigits: 0, // (this suffices for whole numbers, but will print 2500.10 as $2,500.1)
  //maximumFractionDigits: 0, // (causes 2500.99 to be printed as $2,501)
});

///// refs, provide or inject then variables /////

///// computed /////
const amount = computed(() => {
  return formatter.format(props.amount);
});

///// methods /////

///// watchers /////

///// lifecycle /////
</script>
