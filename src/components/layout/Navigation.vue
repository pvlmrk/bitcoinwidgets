<script setup>
import { computed, ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
const currentPath = computed(() => route.path)
const isMenuOpen = ref(false)

const handleNavigation = () => {
  isMenuOpen.value = false
}
</script>

<template>
  <nav class="w-full h-[120px] items-center flex relative z-50">
    <div class="container mx-auto px-6 py-4 flex justify-between items-center">
      <RouterLink to="/" class="font-inter font-bold text-2xl">
        Bitcoin Widgets
      </RouterLink>

      <div class="hidden sm:flex items-center gap-2">
        <RouterLink 
          to="/" 
          class="px-3 py-2 rounded-md font-inter text-sm transition-colors"
          :class="currentPath === '/' ? 'bg-gray-100' : 'hover:bg-gray-50'"
        >
          Home
        </RouterLink>
        <RouterLink 
          to="/generate" 
          class="px-3 py-2 rounded-md font-inter text-sm transition-colors"
          :class="currentPath === '/generate' ? 'bg-gray-100' : 'hover:bg-gray-50'"
        >
          Generate
        </RouterLink>
      </div>

      <button 
        class="sm:hidden p-2"
        @click="isMenuOpen = !isMenuOpen"
      >
        <div class="w-6 h-0.5 bg-black mb-1.5"></div>
        <div class="w-6 h-0.5 bg-black mb-1.5"></div>
        <div class="w-6 h-0.5 bg-black"></div>
      </button>
    </div>

    <div 
      v-if="isMenuOpen"
      class="fixed inset-0 bg-white z-40"
    >
      <div class="container mx-auto px-6 py-4 flex justify-between items-center">
        <RouterLink @click="handleNavigation" to="/" class="font-inter font-bold text-2xl">
          Bitcoin Widgets
        </RouterLink>
        
        <button 
          class="p-2"
          @click="isMenuOpen = false"
        >
          <div class="w-6 h-0.5 bg-black rotate-45 translate-y-0.5 absolute"></div>
          <div class="w-6 h-0.5 bg-black -rotate-45 translate-y-0.5 absolute"></div>
        </button>
      </div>

      <div class="flex flex-col items-center justify-center h-[calc(100vh-120px)]">
        <RouterLink 
          to="/" 
          class="px-3 py-4 text-xl font-medium transition-colors"
          :class="currentPath === '/' ? 'text-black' : 'text-gray-500 hover:text-black'"
          @click="handleNavigation"
        >
          Home
        </RouterLink>
        <RouterLink 
          to="/generate" 
          class="px-3 py-4 text-xl font-medium transition-colors"
          :class="currentPath === '/generate' ? 'text-black' : 'text-gray-500 hover:text-black'"
          @click="handleNavigation"
        >
          Generate
        </RouterLink>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.fixed {
  animation: fadeIn 0.2s ease-out;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>