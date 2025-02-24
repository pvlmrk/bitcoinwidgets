<template>
  <button
    class="inline-flex items-center justify-center whitespace-nowrap rounded-md text-sm font-medium transition-all focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50 relative overflow-hidden group"
    :class="[
      variants[variant],
      sizes[size],
      className
    ]"
    :disabled="disabled"
    :type="type"
    v-bind="$attrs"
  >
    <span class="relative z-10 flex items-center justify-center gap-2">
      <slot name="icon-left"></slot>
      <slot></slot>
      <slot name="icon-right"></slot>
    </span>
    <span 
      v-if="variant === 'bitcoin'" 
      class="absolute inset-0 bg-white opacity-0 group-hover:opacity-20 transition-opacity duration-300"
    ></span>
    <span 
      v-if="variant === 'bitcoin'"
      class="absolute -inset-px rounded-md opacity-0 group-hover:opacity-100 transition-opacity duration-300 bg-gradient-to-r from-bitcoin-orange/20 to-bitcoin-light/20 blur-sm"
    ></span>
  </button>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  variant: {
    type: String,
    default: 'default',
    validator: (value) => {
      return ['default', 'destructive', 'outline', 'secondary', 'ghost', 'link', 'bitcoin'].includes(value)
    }
  },
  size: {
    type: String,
    default: 'default',
    validator: (value) => {
      return ['default', 'sm', 'lg', 'icon'].includes(value)
    }
  },
  disabled: {
    type: Boolean,
    default: false
  },
  type: {
    type: String,
    default: 'button'
  },
  className: {
    type: String,
    default: ''
  }
})

const variants = computed(() => ({
  default: 'bg-slate-900 text-slate-50 hover:bg-slate-800 active:bg-slate-700',
  destructive: 'bg-red-500 text-slate-50 hover:bg-red-600 active:bg-red-700',
  outline: 'border border-slate-200 bg-white hover:bg-slate-50 hover:text-slate-900 active:bg-slate-100',
  secondary: 'bg-slate-100 text-slate-900 hover:bg-slate-200 active:bg-slate-300',
  ghost: 'hover:bg-slate-100 hover:text-slate-900',
  link: 'text-slate-900 underline-offset-4 hover:underline',
  bitcoin: 'bg-gradient-bitcoin text-white hover:shadow-md active:shadow-glow transition-shadow duration-300'
}))

const sizes = computed(() => ({
  default: 'h-11 px-6 py-2',
  sm: 'h-9 rounded-md px-3',
  lg: 'h-12 rounded-md px-8',
  icon: 'h-10 w-10'
}))
</script>