<script setup>
import { ref, computed, onMounted, watch } from 'vue'
import { Button } from "@/components/ui/button"
import { Input } from "@/components/ui/input"
import ColorPicker from "@/components/ui/ColorPicker.vue"
import BitcoinWidget from "@/components/BitcoinWidget.vue"

const widgetData = ref({
  name: '',
  description: '',
  address: '',
  image: '',
  accent: '#F7931A' // Default to Bitcoin orange
})

const copied = ref(false)
const isSaving = ref(false)
const widgetSaved = ref(false)
const widgetPresets = ref([
  {
    name: 'Satoshi Nakamoto',
    description: 'Creator of Bitcoin',
    address: '',
    image: 'https://cdn.britannica.com/37/238937-050-45D054F6/Bitcoin-inventor-Satoshi-Nakamoto-pictured-on-a-coin.jpg',
    accent: '#5ECFC7'
  },
  {
    name: 'Elon Musk',
    description: 'Tesla, SpaceX, X',
    address: '',
    image: 'https://pbs.twimg.com/profile_images/1893803697185910784/Na5lOWi5_400x400.jpg',
    accent: '#000000'
  },
  {
    name: 'Donald Trump',
    description: 'President of the United States',
    address: '',
    image: 'https://pbs.twimg.com/profile_images/1881368435453542400/NnD56DYV_400x400.jpg',
    accent: '#0038a3'
  },
])

const updateColor = (color) => {
  widgetData.value.accent = color
}

const codePreview = computed(() => {
  return `<bitcoin-widget
  name="${widgetData.value.name || 'Bitcoin Widgets'}"
  description="${widgetData.value.description || 'Start accepting bitcoin donations on your website'}"
  address="${widgetData.value.address || ''}"
  image="${widgetData.value.image || ''}"
  accent="${widgetData.value.accent}"
/>
<script src="${window.location.origin}/app.js"><\/script>`
})

const copyCode = async () => {
  await navigator.clipboard.writeText(codePreview.value)
  copied.value = true
  setTimeout(() => {
    copied.value = false
  }, 1500)
}

const saveWidget = () => {
  isSaving.value = true
  
  // Simulate API call
  setTimeout(() => {
    isSaving.value = false
    widgetSaved.value = true
    
    // Reset saved state after 2 seconds
    setTimeout(() => {
      widgetSaved.value = false
    }, 2000)
    
    // Save to localStorage as an example
    const savedWidgets = JSON.parse(localStorage.getItem('savedWidgets') || '[]')
    savedWidgets.push({
      ...widgetData.value,
      id: Date.now(),
      createdAt: new Date().toISOString()
    })
    localStorage.setItem('savedWidgets', JSON.stringify(savedWidgets))
  }, 800)
}

const usePreset = (preset) => {
  widgetData.value = { ...preset }
}



// Watch for changes to provide visual feedback
watch(widgetData, () => {
  // Reset any success states
  widgetSaved.value = false
}, { deep: true })
</script>

<template>
  <main class="bg-gradient-to-b from-slate-50 to-white">
    <div class="container mx-auto px-6 py-12 max-w-[1400px]">
      <!-- Header with animated underline -->
      <div class="text-center max-w-3xl mx-auto mb-12 animate-slide-up">
        <h1 class="text-[32px] sm:text-[38px] font-bold mb-4 relative inline-block">
          Create your bitcoin widget
          <span class="absolute -bottom-2 left-0 h-[4px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
        </h1>
        <p class="text-slate-600 text-[18px] mt-6">
          Fill out the details and make this widget truly yours with easy customization.
        </p>
      </div>

      <!-- Quick presets -->
      <div class="mb-12 bg-white p-6 rounded-xl shadow-sm border border-slate-100 animate-fade-in">
        <h2 class="font-medium text-lg mb-4">Quick presets</h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <div 
            v-for="(preset, index) in widgetPresets" 
            :key="index"
            class="p-4 rounded-lg border border-slate-200 hover:border-bitcoin-orange/50 transition-all duration-200 cursor-pointer hover:shadow-md group"
            @click="usePreset(preset)"
          >
            <div class="flex items-center gap-3 mb-2">
              <div 
                class="w-8 h-8 rounded-full bg-slate-100 flex-shrink-0 overflow-hidden"
                :style="{ backgroundColor: preset.accent }"
              >
                <img v-if="preset.image" :src="preset.image" alt="" class="w-full h-full object-cover" />
              </div>
              <div>
                <h3 class="font-medium text-slate-900">{{ preset.name }}</h3>
                <p class="text-xs text-slate-500">{{ preset.description }}</p>
              </div>
            </div>
            <div class="flex justify-center mt-2">
              <span class="text-xs px-2 py-1 rounded bg-slate-100 text-slate-600 group-hover:bg-bitcoin-orange/10 group-hover:text-bitcoin-orange transition-colors">Use preset</span>
            </div>
          </div>
        </div>
      </div>

      <!-- Form fields -->
      <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100 space-y-8 mb-12 animate-fade-in">
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
          <div class="relative group input-focus-indicator">
            <label class="block font-medium mb-2 text-slate-800">Name</label>
            <Input 
              v-model="widgetData.name" 
              type="text" 
              placeholder="Enter your name or organization" 
              class="w-full bg-white transition-all" 
            />
            <p class="mt-1 text-xs text-slate-500">This appears as the title of your widget</p>
          </div>

          <div class="relative group input-focus-indicator">
            <label class="block font-medium mb-2 text-slate-800">Description</label>
            <Input 
              v-model="widgetData.description" 
              type="text" 
              placeholder="Enter a short bio or tagline" 
              class="w-full bg-white transition-all" 
            />
            <p class="mt-1 text-xs text-slate-500">Briefly describe yourself or your project</p>
          </div>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
          <div class="relative group input-focus-indicator">
            <label class="block font-medium mb-2 text-slate-800">Bitcoin address</label>
            <Input 
              v-model="widgetData.address" 
              type="text" 
              placeholder="Enter your bitcoin address" 
              class="w-full bg-white transition-all font-mono text-sm" 
            />
            <p class="mt-1 text-xs text-slate-500">Your Bitcoin address where donations will be sent</p>
          </div>

          <div class="relative group input-focus-indicator">
            <label class="block font-medium mb-2 text-slate-800">Profile picture URL</label>
            <Input 
              v-model="widgetData.image" 
              type="text" 
              placeholder="Enter image URL (optional)" 
              class="w-full bg-white transition-all" 
            />
            <p class="mt-1 text-xs text-slate-500">URL to your profile image or logo</p>
          </div>
        </div>

        <div>
          <label class="block font-medium mb-4 text-slate-800">Widget color</label>
          <ColorPicker 
            v-model="widgetData.accent" 
            @update:modelValue="(color) => widgetData.accent = color" 
          />
          <p class="mt-2 text-xs text-slate-500">This color will be used as the accent for your widget</p>
        </div>
        
        <div class="flex justify-end pt-4">
          <Button 
            @click="saveWidget" 
            variant="bitcoin"
            class="relative overflow-hidden"
            :disabled="isSaving || !widgetData.address"
          >
            <span v-if="isSaving">
              <svg class="animate-spin -ml-1 mr-2 h-4 w-4 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
                <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
              </svg>
              Saving...
            </span>
            <span v-else-if="widgetSaved" class="flex items-center">
              <svg class="h-4 w-4 text-white mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
              </svg>
              Saved!
            </span>
            <span v-else>Save widget</span>
          </Button>
        </div>
      </div>

      <!-- Preview and code section -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12 animate-fade-in">
        <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100">
          <h2 class="font-bold text-xl mb-6 relative inline-block">
            Widget preview
            <span class="absolute -bottom-1 left-0 h-[2px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
          </h2>
          
          <p class="text-slate-500 text-sm mb-8">
            This is how your widget will look like on your website.
          </p>

          <div class="flex justify-center p-4 bg-slate-50 rounded-lg">
            <div class="relative transform hover:scale-[1.02] transition-transform duration-300">
              <!-- Glow effect (subtle) -->
              <div class="absolute -inset-1 bg-gradient-to-r from-slate-200 to-white rounded-xl blur-sm opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
              
              <!-- Widget -->
              <bitcoin-widget 
                :name="widgetData.name || 'Bitcoin Widgets'"
                :description="widgetData.description || 'Start accepting bitcoin donations on your website'"
                :address="widgetData.address || '1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa'"
                :image="widgetData.image || '/path/to/default.jpg'" 
                :accent="widgetData.accent" 
              />
            </div>
          </div>
        </div>

        <div class="bg-white p-6 rounded-xl shadow-sm border border-slate-100 relative">
          <h2 class="font-bold text-xl mb-6 relative inline-block">
            Your HTML code
            <span class="absolute -bottom-1 left-0 h-[2px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
          </h2>
          
          <p class="text-slate-500 text-sm mb-4">
            Copy this code and paste it into your website to embed the widget.
          </p>
          
          <div class="relative">
            <pre class="bg-slate-50 p-4 font-mono rounded-lg text-sm whitespace-pre border border-slate-100 overflow-x-auto max-h-[343px] mb-6 break-all">{{ codePreview }}</pre>
            
            <button 
              @click="copyCode" 
              :class="[
                'absolute top-[6px] right-[6px] px-3 py-1.5 text-sm rounded-md transition-all duration-200 flex items-center gap-1.5 shadow-sm',
                copied
                  ? 'bg-green-500 text-white'
                  : 'bg-slate-800 hover:bg-slate-700 text-white'
              ]"
              :disabled="copied"
            >
              <span v-if="copied" class="flex items-center">
                <svg class="h-4 w-4 text-white mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                </svg>
                Copied!
              </span>
              <span v-else class="flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1">
                  <rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect>
                  <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path>
                </svg>
                Copy code
              </span>
            </button>
          </div>
          
          <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
            <div class="flex items-start gap-3">
              <div class="mt-1 text-bitcoin-orange">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <circle cx="12" cy="12" r="10"></circle>
                  <line x1="12" y1="8" x2="12" y2="12"></line>
                  <line x1="12" y1="16" x2="12.01" y2="16"></line>
                </svg>
              </div>
              <div>
                <h4 class="font-medium text-sm text-slate-900 mb-1">Integration instructions</h4>
                <p class="text-xs text-slate-600">
                  Copy the code above and paste it where you want the widget to appear on your site. 
                  The script tag loads our widget library automatically.
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.copied-animation {
  animation: pop 0.3s ease-in-out;
}

@keyframes pop {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}

@media (max-width: 767px) {
  .grid-cols-2 {
    grid-template-columns: 1fr;
  }
}


</style>