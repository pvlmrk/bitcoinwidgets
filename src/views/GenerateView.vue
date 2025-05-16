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
  image: 'https://bitcoin.org/img/icons/opengraph.png',  // Using Bitcoin's official logo
  accent: '#F7931A' // Default to Bitcoin orange
})

const copied = ref(false)
const isSaving = ref(false)
const widgetSaved = ref(false)
const savedWidgets = ref([])
const showSavedDialog = ref(false)

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

const loadSavedWidgets = () => {
  const widgets = JSON.parse(localStorage.getItem('savedWidgets') || '[]')
  savedWidgets.value = widgets
  showSavedDialog.value = true
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
    const savedWidgetsData = JSON.parse(localStorage.getItem('savedWidgets') || '[]')
    const newWidget = {
      ...widgetData.value,
      id: Date.now(),
      createdAt: new Date().toISOString()
    }
    savedWidgetsData.push(newWidget)
    localStorage.setItem('savedWidgets', JSON.stringify(savedWidgetsData))
    
    // Update the savedWidgets ref if dialog is open
    if (showSavedDialog.value) {
      savedWidgets.value.push(newWidget)
    }
  }, 800)
}

const usePreset = (preset) => {
  widgetData.value = { ...preset }
  showSavedDialog.value = false
}

const deleteWidget = (id, event) => {
  event.stopPropagation(); // Prevent clicking on the parent widget
  
  // Remove from local ref
  savedWidgets.value = savedWidgets.value.filter(widget => widget.id !== id);
  
  // Remove from localStorage
  const widgets = JSON.parse(localStorage.getItem('savedWidgets') || '[]');
  const updatedWidgets = widgets.filter(widget => widget.id !== id);
  localStorage.setItem('savedWidgets', JSON.stringify(updatedWidgets));
}

// Close dialog when clicking outside
const closeOnOutsideClick = (e) => {
  if (e.target.classList.contains('modal-overlay')) {
    showSavedDialog.value = false
  }
}

// Watch for changes to provide visual feedback
watch(widgetData, () => {
  // Reset any success states
  widgetSaved.value = false
}, { deep: true })
</script>

<template>
  <main>
    <div class="container mx-auto px-6 py-12 max-w-[1400px]">
      <!-- Header with animated underline -->
      <header class="text-center max-w-3xl mx-auto mb-12 animate-slide-up">
        <h1 class="text-[24px] sm:text-[28px] md:text-[32px] font-bold mb-4 relative inline-block">
          Create your bitcoin widget
          <span class="absolute -bottom-2 left-0 h-[4px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
        </h1>
        <p class="text-slate-600 text-base sm:text-lg md:text-[18px] mt-6">
          Fill out the details and make this widget truly yours with easy customization.
        </p>
      </header>

      <!-- Quick presets -->
      <section class="mb-6 bg-white p-6 rounded-xl shadow-sm border border-slate-100 animate-fade-in" aria-labelledby="presets-heading">
        <h2 id="presets-heading" class="font-bold text-lg sm:text-xl mb-6 relative inline-block">
          Quick presets
          <span class="absolute -bottom-1 left-0 h-[2px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
          <button 
            v-for="(preset, index) in widgetPresets" 
            :key="index"
            class="p-4 flex justify-between items-center rounded-lg border border-slate-200 hover:border-bitcoin-orange/50 transition-all duration-200 cursor-pointer hover:shadow-md group"
            @click="usePreset(preset)"
          >
            <div class="flex flex-wrap items-center gap-3 mb-2">
              <div 
                class="w-8 h-8 rounded-full bg-slate-100 flex-shrink-0 overflow-hidden"
                :style="{ backgroundColor: preset.accent }"
                aria-hidden="true"
              >
                <img v-if="preset.image" :src="preset.image" :alt="preset.name" class="w-full h-full object-cover" />
              </div>
              <div class="text-left">
                <h3 class="font-medium text-slate-900">{{ preset.name }}</h3>
                <p class="text-xs text-slate-500">{{ preset.description }}</p>
              </div>
            </div>
            <div class="flex justify-center mt-2">
              <span class="text-xs px-2 py-1 rounded bg-slate-100 text-slate-600 group-hover:bg-bitcoin-orange/10 group-hover:text-bitcoin-orange transition-colors">Use preset</span>
            </div>
          </button>
        </div>
      </section>

      <!-- Form fields -->
      <form class="bg-white p-6 rounded-xl shadow-sm border border-slate-100 space-y-8 mb-6 animate-fade-in" aria-labelledby="form-heading">
        <h2 id="form-heading" class="font-bold text-lg sm:text-xl relative inline-block">
          Fill out the form
          <span class="absolute -bottom-1 left-0 h-[2px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
        </h2>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-8">
          <div class="relative group input-focus-indicator">
            <label for="widget-name" class="block font-medium mb-2 text-slate-800">Name</label>
            <Input 
              id="widget-name"
              v-model="widgetData.name" 
              type="text" 
              placeholder="Enter your name or organization" 
              class="w-full bg-white transition-all" 
            />
            <p class="mt-1 text-xs text-slate-500">This appears as the title of your widget</p>
          </div>

          <div class="relative group input-focus-indicator">
            <label for="widget-description" class="block font-medium mb-2 text-slate-800">Description</label>
            <Input 
              id="widget-description"
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
            <label for="widget-address" class="block font-medium mb-2 text-slate-800">Bitcoin address</label>
            <Input 
              id="widget-address"
              v-model="widgetData.address" 
              type="text" 
              placeholder="Enter your bitcoin address" 
              class="w-full bg-white transition-all text-sm" 
            />
            <p class="mt-1 text-xs text-slate-500">Your Bitcoin address where donations will be sent</p>
          </div>

          <div class="relative group input-focus-indicator">
            <label for="widget-image" class="block font-medium mb-2 text-slate-800">Profile picture URL</label>
            <Input 
              id="widget-image"
              v-model="widgetData.image" 
              type="text" 
              placeholder="Enter image URL (optional)" 
              class="w-full bg-white transition-all" 
            />
            <p class="mt-1 text-xs text-slate-500">URL to your profile image or logo</p>
          </div>
        </div>

        <div>
          <label for="widget-color" class="block font-medium mb-4 text-slate-800">Widget color</label>
          <div class="flex justify-between items-end">
            <ColorPicker 
              id="widget-color"
              v-model="widgetData.accent" 
              @update:modelValue="(color) => widgetData.accent = color" 
            />
            <div class="flex flex-wrap justify-end gap-3">
              <Button 
                @click="loadSavedWidgets" 
                variant="outline"
                class="relative overflow-hidden hover:border-bitcoin-orange/50 transition-all"
                type="button"
              >
                <span class="flex items-center">
                  <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-2" aria-hidden="true">
                    <path d="M4 22h14a2 2 0 0 0 2-2V7.5L14.5 2H6a2 2 0 0 0-2 2v4"></path>
                    <polyline points="14 2 14 8 20 8"></polyline>
                    <path d="M2 15h10"></path>
                    <path d="m9 18 3-3-3-3"></path>
                  </svg>
                  Saved Widgets
                </span>
              </Button>
  
              <Button 
                @click="saveWidget" 
                variant="bitcoin"
                class="relative overflow-hidden"
                :disabled="isSaving || !widgetData.address"
                type="button"
              >
                <span v-if="isSaving">
                  <svg class="animate-spin -ml-1 mr-2 h-4 w-4 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" aria-hidden="true">
                    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
                    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
                  </svg>
                  Saving...
                </span>
                <span v-else-if="widgetSaved" class="flex items-center">
                  <svg class="h-4 w-4 text-white mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                  </svg>
                  Saved!
                </span>
                <span v-else>Save widget</span>
              </Button>
            </div>
          </div>
        </div>
      </form>

      <!-- Preview and code section -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 animate-fade-in">
        <section class="bg-white p-6 rounded-xl shadow-sm border border-slate-100" aria-labelledby="preview-heading">
          <h2 id="preview-heading" class="font-bold text-lg sm:text-xl mb-6 relative inline-block">
            Widget preview
            <span class="absolute -bottom-1 left-0 h-[2px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
          </h2>
          
          <p class="text-slate-500 text-sm mb-8">
            This is how your widget will look like on your website.
          </p>

          <div class="flex justify-center p-4 bg-slate-50 rounded-lg">
            <div class="relative">
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
        </section>

        <section class="bg-white p-6 rounded-xl shadow-sm border border-slate-100 relative" aria-labelledby="code-heading">
          <h2 id="code-heading" class="font-bold text-lg sm:text-xl mb-6 relative inline-block">
            Your HTML code
            <span class="absolute -bottom-1 left-0 h-[2px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
          </h2>
          
          <p class="text-slate-500 text-sm mb-4">
            Copy this code and paste it into your website to embed the widget.
          </p>
          
          <div class="relative">
            <pre id="code-preview" class="bg-slate-50 p-4 font-sans rounded-lg text-sm whitespace-pre border border-slate-100 overflow-x-auto max-h-[343px] mb-4 break-all code-scrollbar" aria-label="HTML code for embedding the widget">{{ codePreview }}</pre>
            
            <button 
              @click="copyCode" 
              :class="[
                'absolute top-[6px] right-[6px] px-3 py-1.5 text-sm rounded-md transition-all duration-200 flex items-center gap-1.5 shadow-sm',
                copied
                  ? 'bg-green-500 text-white'
                  : 'bg-slate-800 hover:bg-slate-700 text-white'
              ]"
              :disabled="copied"
              :aria-label="copied ? 'Code copied to clipboard' : 'Copy code to clipboard'"
            >
              <span v-if="copied" class="flex items-center">
                <svg class="h-4 w-4 text-white mr-1" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
                </svg>
                Copied!
              </span>
              <span v-else class="flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="mr-1" aria-hidden="true">
                  <rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect>
                  <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"></path>
                </svg>
                Copy code
              </span>
            </button>
          </div>
          
          <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
            <div class="flex items-start gap-3">
              <div class="mt-1 text-bitcoin-orange" aria-hidden="true">
                <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                  <circle cx="12" cy="12" r="10"></circle>
                  <line x1="12" y1="8" x2="12" y2="12"></line>
                  <line x1="12" y1="16" x2="12.01" y2="16"></line>
                </svg>
              </div>
              <div>
                <h3 class="font-medium text-sm text-slate-900 mb-1">Integration instructions</h3>
                <p class="text-xs text-slate-600">
                  Copy the code above and paste it where you want the widget to appear on your site. 
                  The script tag loads our widget library automatically.
                </p>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
    <div v-if="showSavedDialog" class="fixed inset-0 bg-black bg-opacity-30 dark:bg-black dark:bg-opacity-50 z-50 flex items-center justify-center p-6 modal-overlay backdrop-blur-sm" @click="closeOnOutsideClick">
      <div class="bg-white dark:bg-slate-800 rounded-xl shadow-lg dark:shadow-slate-900/70 max-w-md w-full max-h-[90vh] overflow-hidden animate-fade-in" @click.stop>
        <!-- Dialog Header -->
        <div class="p-6 border-b border-slate-100 dark:border-slate-700">
          <h2 class="text-xl font-bold relative inline-block dark:text-white">
            My Saved Widgets
            <span class="absolute -bottom-1 left-0 h-[2px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
          </h2>
          <p class="text-slate-600 dark:text-slate-300 mt-4 text-sm">
            Your previously saved Bitcoin widgets.
          </p>
        </div>
        
        <!-- Dialog Content -->
        <div class="p-6 dark:bg-slate-800">
          <div v-if="savedWidgets.length === 0" class="text-center py-10">
            <div class="text-bitcoin-orange mb-4 flex justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                <rect x="3" y="3" width="18" height="18" rx="2" ry="2"></rect>
                <line x1="9" y1="3" x2="9" y2="21"></line>
              </svg>
            </div>
            <p class="text-slate-700 dark:text-slate-200 text-lg font-medium">No saved widgets yet</p>
            <p class="text-slate-500 dark:text-slate-400 mt-2">Save a widget to see it here for future use.</p>
          </div>
          
          <div v-else class="space-y-4 max-h-[300px] overflow-y-auto pr-2 custom-scrollbar dark:custom-scrollbar-dark">
            <div 
              v-for="widget in savedWidgets" 
              :key="widget.id"
              class="p-4 rounded-lg border border-slate-200 dark:border-slate-600 hover:border-bitcoin-orange/50 dark:hover:border-bitcoin-orange/70 transition-all duration-200 cursor-pointer hover:shadow-md dark:hover:shadow-slate-900/80 relative dark:bg-slate-700 group"
              @click="usePreset(widget)"
            >
              <button 
                @click="deleteWidget(widget.id, $event)"
                class="absolute top-2 right-2 p-1 rounded-full hover:bg-slate-100 dark:hover:bg-slate-600 transition-colors z-10"
                title="Delete widget"
              >
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-slate-500 hover:text-red-500 dark:text-slate-400 dark:hover:text-red-400">
                  <line x1="18" y1="6" x2="6" y2="18"></line>
                  <line x1="6" y1="6" x2="18" y2="18"></line>
                </svg>
              </button>
              
              <div class="flex items-center gap-4">
                <div 
                  class="w-12 h-12 rounded-full bg-slate-100 dark:bg-slate-600 flex-shrink-0 overflow-hidden"
                  :style="{ backgroundColor: widget.accent }"
                >
                  <img v-if="widget.image" :src="widget.image" alt="" class="w-full h-full object-cover" />
                </div>
                <div>
                  <h3 class="font-medium text-slate-900 dark:text-slate-100 text-lg">{{ widget.name || 'Unnamed Widget' }}</h3>
                  <p class="text-sm text-slate-600 dark:text-slate-300">{{ widget.description || 'No description' }}</p>
                  <p class="text-xs text-slate-400 dark:text-slate-500 mt-1">
                    Saved on {{ new Date(widget.createdAt).toLocaleDateString() }}
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- Dialog Footer -->
        <div class="p-6 border-t border-slate-100 dark:border-slate-700 flex justify-between items-center dark:bg-slate-800">
          <p class="text-xs text-slate-500 dark:text-slate-400 hidden sm:block">Click on a widget to load it</p>
          <Button @click="showSavedDialog = false" variant="outline" class="w-full sm:w-auto dark:bg-slate-700 dark:text-slate-200 dark:border-slate-600 dark:hover:bg-slate-600 dark:hover:border-slate-500 dark:focus:ring-slate-400/50">
            Close
          </Button>
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

.modal-overlay {
  backdrop-filter: blur(2px);
}

.custom-scrollbar::-webkit-scrollbar,
.code-scrollbar::-webkit-scrollbar {
  width: 6px;
  height: 6px;
}

.custom-scrollbar::-webkit-scrollbar-track,
.code-scrollbar::-webkit-scrollbar-track {
  background: #f1f5f9;
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb,
.code-scrollbar::-webkit-scrollbar-thumb {
  background: #cbd5e1;
  border-radius: 10px;
}

.custom-scrollbar::-webkit-scrollbar-thumb:hover,
.code-scrollbar::-webkit-scrollbar-thumb:hover {
  background: #94a3b8;
}
</style>
