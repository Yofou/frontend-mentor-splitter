<template>
  <label class="w-full flex flex-col gap-[.38rem]">
    <span v-if="$slots.default" class="font-spaceMono text-[1rem] font-bold text-[#5E7A7D]">
      <slot />
    </span>
    <span class="relative">
      <span class="absolute top-1/2 -translate-y-1/2 left-[1.2rem]">
        <slot name="icon" />
      </span>
      <input
        type="text"
        class="bg-[#F3F9FA] rounded-[0.3125rem] w-full px-4 py-[0.38rem] text-right text-[1.5rem] font-bold font-spaceMono text-[#00474B] focus:outline-2 outline-[#26C2AE] placeholder:text-[#00474B]/35"
        ref="el"
        :class="{ 'pl-[3rem]': $slots.icon, 'placeholder:text-[#547878] px-[.88rem]': isCustom }"
        :placeholder="placeholder"
      />
    </span>
  </label>
</template>

<script setup lang="ts">
import { onMounted, watch } from "vue";
import { useIMask } from "vue-imask";

///// props/emits /////
const props = defineProps<{
  modelValue?: number;
  scale?: number;
  min?: number;
  max?: number;
  placeholder?: string;
  isCustom?: boolean;
}>();

const emits = defineEmits<{
  (e: "update:modelValue", value: number): void;
}>();

///// refs, provide or inject then variables /////
const { el, typed, unmasked } = useIMask(
  {
    mask: Number,

    scale: props.scale ?? 2,
    thousandsSeparator: ",",
    radix: ".", // fractional delimiter
    mapToRadix: ["."], // symbols to process as radix
    min: props.min ?? 0,
    max: props.max,
  },
  {
    onAccept: (e) => {
      if (e) {
        emits("update:modelValue", typed.value);
      }
    }
  }
);

///// computed /////

///// methods /////

///// watchers /////
watch(
  () => props.modelValue,
  () => {
    if (props.modelValue != null) {
      typed.value = props.modelValue;
    } else {
      unmasked.value = ''
    }
  }
);

onMounted(() => {
  if (props.modelValue != null) {
    typed.value = props.modelValue;
  }
});

///// lifecycle /////
</script>
