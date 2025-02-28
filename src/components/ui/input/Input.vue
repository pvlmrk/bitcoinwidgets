<template>
  <div class="relative">
    <input
      class="flex h-11 w-full rounded-md border border-slate-200 bg-white px-4 py-2 text-sm ring-offset-white transition duration-200 file:border-0 file:bg-transparent file:text-sm file:font-medium placeholder:text-slate-500 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-bitcoin-orange/30 focus-visible:ring-offset-2 focus:border-bitcoin-orange/50 disabled:cursor-not-allowed disabled:opacity-50"
      :class="className"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      v-bind="$attrs"
    />
  </div>
</template>

<script setup>
defineProps({
  modelValue: {
    type: [String, Number],
    default: ''
  },
  className: {
    type: String,
    default: ''
  }
})

defineEmits(['update:modelValue'])
</script>