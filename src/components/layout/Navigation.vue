<template>
  <header class="w-full h-[120px] items-center flex relative z-50">
    <div class="container mx-auto px-6 py-4 flex justify-between items-center">
      <RouterLink to="/" class="group font-inter font-bold text-xl sm:text-2xl flex items-center relative overflow-hidden" aria-label="Bitcoin Widgets Home">
        <span class="flex items-center">
          <span class="text-bitcoin-orange" aria-hidden="true">₿</span>itcoin <span class="text-slate-800">Widgets</span>
        </span>
        <span class="absolute bottom-0 left-0 h-[2px] w-0 bg-gradient-bitcoin group-hover:w-full transition-all duration-300" aria-hidden="true"></span>
      </RouterLink>

      <nav class="hidden sm:flex items-center gap-2" aria-label="Main navigation">
        <RouterLink 
          to="/" 
          class="px-4 py-2 rounded-md font-inter text-sm transition-all duration-200 relative overflow-hidden dark:hover:text-white"
          :class="currentPath === '/' ? 'text-bitcoin-orange font-medium' : 'text-slate-800 hover:text-slate-900'"
          aria-current="currentPath === '/' ? 'page' : undefined"
        >
          <span>Home</span>
          <span class="absolute bottom-0 left-0 h-[2px] w-0 bg-gradient-bitcoin hover:w-full transition-all duration-300"
                :class="currentPath === '/' ? 'w-full' : 'w-0'" aria-hidden="true"></span>
        </RouterLink>
        <RouterLink 
          to="/generate" 
          class="px-4 py-2 rounded-md font-inter text-sm transition-all duration-200 relative overflow-hidden dark:hover:text-white"
          :class="currentPath === '/generate' ? 'text-bitcoin-orange font-medium' : 'text-slate-800 hover:text-slate-900'"
          aria-current="currentPath === '/generate' ? 'page' : undefined"
        >
          <span>Generate</span>
          <span class="absolute bottom-0 left-0 h-[2px] w-0 bg-gradient-bitcoin hover:w-full transition-all duration-300"
                :class="currentPath === '/generate' ? 'w-full' : 'w-0'" aria-hidden="true"></span>
        </RouterLink>
        
        <a 
          href="https://github.com/pvlmrk/bitcoinwidgets" 
          target="_blank"
          rel="noopener noreferrer"
          class="ml-2 p-2 text-slate-700 hover:text-slate-900 transition-colors duration-200 dark:hover:text-white"
          aria-label="View on GitHub"
        >
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
            <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path>
          </svg>
        </a>
        
        <div class="theme-switcher ml-2">
          <ThemeSwitcher />
        </div>
      </nav>

      <button 
        class="sm:hidden p-2 relative z-50 group"
        @click="isMenuOpen = !isMenuOpen"
        aria-expanded="isMenuOpen"
        aria-controls="mobile-menu"
        aria-label="Toggle menu"
      >
        <div class="w-6 h-0.5 bg-black mb-1.5 transition-all duration-300"
             :class="isMenuOpen ? 'rotate-45 translate-y-2 bg-bitcoin-orange' : ''" aria-hidden="true"></div>
        <div class="w-6 h-0.5 bg-black mb-1.5 transition-all duration-300"
             :class="isMenuOpen ? 'opacity-0' : 'opacity-100'" aria-hidden="true"></div>
        <div class="w-6 h-0.5 bg-black transition-all duration-300"
             :class="isMenuOpen ? '-rotate-45 -translate-y-2 bg-bitcoin-orange' : ''" aria-hidden="true"></div>
      </button>
    </div>

    <div 
      v-if="isMenuOpen"
      class="fixed inset-0 bg-white z-40 animate-fade-in"
      id="mobile-menu"
      role="dialog"
      aria-modal="true"
      aria-label="Mobile navigation"
    >
      <nav class="flex flex-col items-center justify-center h-[calc(100vh-120px)]" aria-label="Mobile navigation">
        <RouterLink 
          to="/" 
          class="px-3 py-4 text-lg sm:text-xl font-medium transition-all duration-200 relative"
          :class="currentPath === '/' ? 'text-bitcoin-orange' : 'text-slate-700 hover:text-bitcoin-orange'"
          @click="handleNavigation"
          aria-current="currentPath === '/' ? 'page' : undefined"
        >
          <span class="animate-slide-down" style="animation-delay: 0.1s;">Home</span>
          <span class="absolute bottom-0 left-1/2 -translate-x-1/2 h-[2px] w-0 bg-gradient-bitcoin transition-all duration-300"
                :class="currentPath === '/' ? 'w-1/2' : 'w-0'" aria-hidden="true"></span>
        </RouterLink>
        <RouterLink 
          to="/generate" 
          class="px-3 py-4 text-lg sm:text-xl font-medium transition-all duration-200 relative"
          :class="currentPath === '/generate' ? 'text-bitcoin-orange' : 'text-slate-700 hover:text-bitcoin-orange'"
          @click="handleNavigation"
          aria-current="currentPath === '/generate' ? 'page' : undefined"
        >
          <span class="animate-slide-down" style="animation-delay: 0.2s;">Generate</span>
          <span class="absolute bottom-0 left-1/2 -translate-x-1/2 h-[2px] w-0 bg-gradient-bitcoin transition-all duration-300"
                :class="currentPath === '/generate' ? 'w-1/2' : 'w-0'" aria-hidden="true"></span>
        </RouterLink>
        
        <a 
          href="https://github.com/pvlmrk/bitcoinwidgets" 
          target="_blank"
          rel="noopener noreferrer"
          class="mt-6 p-4 text-slate-700 hover:text-bitcoin-orange transition-colors duration-200 animate-slide-down"
          style="animation-delay: 0.3s;"
          @click="handleNavigation"
        >
          <div class="flex items-center gap-2">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
              <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path>
            </svg>
            GitHub
          </div>
        </a>
        
        <div class="mt-6 animate-slide-down theme-switcher" style="animation-delay: 0.4s;">
          <div class="flex items-center justify-center gap-2 p-2">
            <span class="text-slate-700">Theme:</span>
            <ThemeSwitcher />
          </div>
        </div>
      </nav>
    </div>
  </header>
</template>

<script setup>
import { computed, ref } from 'vue'
import { useRoute } from 'vue-router'
import ThemeSwitcher from '@/components/ui/ThemeSwitcher.vue'

const route = useRoute()
const currentPath = computed(() => route.path)
const isMenuOpen = ref(false)

const handleNavigation = () => {
  isMenuOpen.value = false
}
</script>