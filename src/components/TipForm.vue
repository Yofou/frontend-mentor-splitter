<template>
  <form @submit.prevent class="md:pt-[.81rem] md:pl-4">
    <Input v-model="bill" placeholder="0">
      Bill
      
      <template v-slot:icon>
          <DollarIcon />
      </template>
    </Input>

    <div class="mt-8 md:mt-10 flex flex-col gap-4">
      <p class="text-[1rem] font-bold font-spaceMono text-[#5E7A7D]">Select Tip %</p>

      <RadioGroup v-model="tipPerct" class="grid grid-cols-2 md:grid-cols-3 gap-4 md:gap-x-[.88rem] md:gap-y-4" :disabled="isDoneByCustom">
        <RadioItem :value=".05" @click="onTipSelect">5%</RadioItem>
        <RadioItem :value=".1" @click="onTipSelect">10%</RadioItem>
        <RadioItem :value=".15" @click="onTipSelect">15%</RadioItem>
        <RadioItem :value=".25" @click="onTipSelect">25%</RadioItem>
        <RadioItem :value=".5" @click="onTipSelect">50%</RadioItem>
        <Input v-model="customVModel" placeholder="Custom" :min="0" isCustom />
      </RadioGroup>
    </div>

    <Input class="mt-8 md:mt-10" v-model="numberOfPeople" :scale="0" :min="1" placeholder="0">
      Number of People
      
      <template v-slot:icon>
          <PeopleIcon />
      </template>
    </Input>
  </form>
</template>

<script setup lang="ts">
import Input from './Input.vue';
import DollarIcon from './Icons/Dollar.vue'
import PeopleIcon from './Icons/People.vue'
import { RadioGroup, RadioItem } from './Radio'
import { computed, ref } from 'vue';

///// refs, provide or inject then variables /////
const bill = defineModel<number>('bill')
const numberOfPeople = defineModel<number>('numberOfPeople')
const tipPerct = defineModel<number>('tipPerct')

const isDoneByCustom = ref(false);

///// computed /////
const customVModel = computed({
  get() {
    if (tipPerct.value == null || !isDoneByCustom.value) return undefined;

    return tipPerct.value * 100
  },
  set(value) {
    if (value == null) return;

    isDoneByCustom.value = true;
    tipPerct.value = value / 100
  }
})

///// methods /////
const onTipSelect = () => {
  isDoneByCustom.value = false;
}

///// watchers /////

///// lifecycle /////
</script>
