<script setup>
import { Input } from "@/components/ui/input";
import Footer from "@/components/layout/Footer.vue";
</script>
<template>
  <main class="container mx-auto px-6 py-12 max-w-[1400px]">
    <h1 class="text-[32px] sm:text-[32px] font-bold mb-2">
      Create your bitcoin widget
    </h1>
    <p class="text-gray-500 mb-12">
      Fill out the details and make this widget truly yours with easy
      customization.
    </p>

    <div class="space-y-6 mb-12">
      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
        <div>
          <label class="block font-medium mb-2">Name</label>
          <Input type="text" placeholder="Satoshi Nakamoto" class="w-full bg-white" />
        </div>

        <div>
          <label class="block font-medium mb-2">Receiving address</label>
          <Input type="text" placeholder="your@address.com" class="w-full bg-white" />
        </div>
      </div>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
        <div>
          <label class="block font-medium mb-2">Description</label>
          <Input type="text" placeholder="Creator of Bitcoin" class="w-full bg-white" />
        </div>

        <div>
          <label class="block font-medium mb-2">Profile picture URL</label>
          <Input type="text" placeholder="https://upload.wikimedia.org/wikipedia/commons/thu..."
            class="w-full bg-white" />
        </div>
      </div>

      <div>
        <label class="block font-medium mb-2">Color</label>
        <div class="flex gap-2">
          <div class="w-8 h-8 rounded-md bg-[#40B8F8] cursor-pointer border border-black/5"></div>
        </div>
      </div>
    </div>

    <div class="space-y-12">
      <h2 class="font-bold text-xl">Preview & code</h2>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
        <div>
          <h3 class="font-medium mb-2">Widget preview</h3>
          <p class="text-gray-500 text-sm mb-4">
            How your widget will look like on the web.
          </p>

          <div class="w-full sm:w-[350px] bg-[#40B8F8] rounded-2xl p-6 shadow-widget">
            <div class="flex flex-col items-center text-center">
              <div class="w-20 h-20 rounded-full bg-gray-200 mb-3"></div>
              <div class="text-white font-medium">Satoshi Nakamoto</div>
              <div class="text-white/80 text-sm mb-4">Creator of Bitcoin</div>
              <Button class="w-full bg-white text-black hover:bg-white/90">
                Donate bitcoin
              </Button>
            </div>
          </div>
        </div>

        <div>
          <h3 class="font-medium mb-2">Your HTML code</h3>
          <p class="text-gray-500 text-sm mb-4">
            Copy & paste into your website.
          </p>
          <pre
            class="bg-gray-50 p-4 rounded-lg text-sm font-mono whitespace-pre-wrap border border-gray-100 overflow-x-auto">
&lt;bitcoinwidget 
  name="Satoshi Nakamoto"
  background="#FF751A"
  address="your@bitcoin.com"
  image="https://upload.wikimedia.org/wikipedia/commons/d/d4/Bitcoin.svg"
/&gt;
&lt;script src="https://bitcoin-widgets.com/script.js"&gt;&lt;/script&gt;</pre>
        </div>
      </div>
    </div>
  </main>
  <Footer />
</template>
