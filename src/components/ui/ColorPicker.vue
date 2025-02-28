<template>
  <div class="w-auto p-0">
    <input
      type="color"
      v-model="selectedColor"
      @input="updateColor"
      class="w-12 h-10 cursor-pointer border-0 rounded-md p-1 color-picker-modern"
      :class="{ 'dark': isDarkMode }"
    />
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'

const props = defineProps({
  modelValue: {
    type: String,
    default: "#e9983c"
  }
})

const emit = defineEmits(['update:modelValue'])

const selectedColor = ref(props.modelValue)
const isDarkMode = ref(false)

const updateColor = () => {
  emit('update:modelValue', selectedColor.value)
}

const checkTheme = () => {
  isDarkMode.value = document.documentElement.classList.contains('dark')
}

watch(() => props.modelValue, (newValue) => {
  selectedColor.value = newValue
})

onMounted(() => {
  checkTheme()
  
  const observer = new MutationObserver(checkTheme)
  observer.observe(document.documentElement, {
    attributes: true,
    attributeFilter: ['class']
  })
})
</script>

<style scoped>
input[type="color"] {
  -webkit-appearance: none;
  appearance: none;
  background-color: white;
  border: 1px solid #e2e8f0;
  box-shadow: 0 1px 2px rgba(0, 0, 0, 0.05);
  transition: all 0.2s ease;
}

input[type="color"].dark {
  background-color: #1e293b;
  border: 1px solid #334155;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.2);
}

input[type="color"]::-webkit-color-swatch-wrapper {
  padding: 0;
}

input[type="color"]::-webkit-color-swatch {
  border: none;
  border-radius: 6px;
}

input[type="color"]:hover {
  border-color: #cbd5e1;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
}

input[type="color"].dark:hover {
  border-color: #475569;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
}

input[type="color"]:focus {
  outline: 2px solid #e2e8f0;
  outline-offset: 2px;
}

input[type="color"].dark:focus {
  outline: 2px solid #475569;
  outline-offset: 2px;
}

/* For Firefox support */
input[type="color"]::-moz-color-swatch {
  border: none;
  border-radius: 6px;
}
</style>