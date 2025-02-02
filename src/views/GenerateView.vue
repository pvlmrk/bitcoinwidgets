<script setup>
import { ref, computed } from 'vue'
import { Input } from "@/components/ui/input"
import ColorPicker from "@/components/ui/ColorPicker.vue"
import BitcoinWidget from "@/components/BitcoinWidget.vue"

const widgetData = ref({
  name: '',
  description: '',
  address: '',
  image: '',
  accent: '#1E40AF'
})

const copied = ref(false)

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
</script>

<template>
  <main class="container mx-auto px-6 py-12 max-w-[1400px]">
    <h1 class="text-[32px] sm:text-[32px] font-bold mb-2">
      Create your bitcoin widget
    </h1>
    <!-- Add a helper class "intro" to only center the intro paragraph -->
    <p class="intro text-gray-500 mb-12">
      Fill out the details and make this widget truly yours with easy customization.
    </p>

    <div class="space-y-6 mb-12">
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
        <div>
          <label class="block font-medium mb-2">Name</label>
          <Input v-model="widgetData.name" type="text" placeholder="Enter your name" class="w-full bg-white" />
        </div>

        <div>
          <label class="block font-medium mb-2">Description</label>
          <Input v-model="widgetData.description" type="text" placeholder="Enter your description" class="w-full bg-white" />
        </div>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
        <div>
          <label class="block font-medium mb-2">Bitcoin address</label>
          <Input v-model="widgetData.address" type="text" placeholder="Enter your bitcoin address" class="w-full bg-white" />
        </div>

        <div>
          <label class="block font-medium mb-2">Profile picture URL</label>
          <Input v-model="widgetData.image" type="text" placeholder="Enter your image URL" class="w-full bg-white" />
        </div>
      </div>

      <div>
        <label class="block font-medium mb-2">Widget color</label>
        <div class="flex gap-2">
          <ColorPicker v-model="widgetData.accent" @update:modelValue="(color) => widgetData.accent = color" />
        </div>
      </div>
    </div>

    <div class="space-y-12">
      <h2 class="font-bold text-xl">Preview & code</h2>

      <div class="grid grid-cols-1 md:grid-cols-2 gap-12">
        <div>
          <h3 class="font-medium mb-2">Widget preview</h3>
          <p class="text-gray-500 text-sm mb-4">
            How your widget will look like on the web.
          </p>

          <bitcoin-widget 
            :name="widgetData.name || 'Bitcoin Widgets'"
            :description="widgetData.description || 'Start accepting bitcoin donations on your website'"
            :address="widgetData.address || '1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa'"
            :image="widgetData.image || 'https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/Bitcoin.svg/1024px-Bitcoin.svg.png'" 
            :accent="widgetData.accent" 
          />
        </div>

        <div class="relative">
          <h3 class="font-medium mb-2">Your HTML code</h3>
          <p class="text-gray-500 text-sm mb-4">
            Copy & paste into your website.
          </p>
          <!-- Use whitespace-pre so code doesn't wrap early -->
          <pre class="bg-gray-50 p-4 font-sans rounded-lg text-sm whitespace-pre border border-gray-100 overflow-x-auto max-h-[343px]">
{{ codePreview }}
          </pre>
          <button @click="copyCode" :class="[
            'absolute top-[85px] right-4 px-3 py-1.5 text-sm rounded-md transition-all duration-200 flex items-center gap-1.5',
            copied
              ? 'bg-green-100 text-green-800 border-green-200'
              : 'bg-gray-800 hover:bg-gray-700 text-white'
          ]">
            <span v-if="copied">✅</span>
            <span>{{ copied ? 'Copied!' : 'Copy code' }}</span>
          </button>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
@media (max-width: 887px) {
  h1,
  .intro {
    text-align: center;
  }
}

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
</style>
