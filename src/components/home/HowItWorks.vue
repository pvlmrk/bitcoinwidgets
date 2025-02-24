<template>
  <section class="container mx-auto px-6 mb-24 py-6">
    <div class="text-center max-w-3xl mx-auto mb-16 animate-slide-up">
      <h2 class="text-[32px] font-bold mb-4 relative inline-block">
        How it works
        <span class="absolute -bottom-2 left-0 h-[4px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
      </h2>
      <p class="text-slate-600 text-[18px] mt-6">
        Your widget guides people through 4 stages: profile view, amount entry, QR payment, and success.
      </p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-16 mb-16 max-w-[1000px] mx-auto">
      <!-- Step 1 -->
      <div class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <div class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">1</span>
          <span class="font-bold text-xl text-slate-800">Profile view</span>
        </div>
        <div class="relative w-full transition-all duration-300 transform group-hover:scale-[1.02]">
          <!-- Card glow effect -->
          <div class="absolute inset-0 bg-gradient-to-br from-slate-100 to-white rounded-2xl shadow-md group-hover:shadow-lg transition-all duration-300"></div>
          
          <!-- Step indicator -->
          <div class="absolute -top-3 -right-3 w-6 h-6 rounded-full bg-gradient-bitcoin flex items-center justify-center text-white text-xs font-bold shadow-md">1</div>
          
          <!-- Widget -->
          <div class="relative p-4">
            <bitcoin-widget
              name="Satoshi Nakamoto"
              description="Creator of Bitcoin"
              image="/path/to/satoshi.jpg"
              address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
              accent="#5ECFC7"
              button-text="Donate bitcoin"
              initial-step="start"
            />
          </div>
        </div>
      </div>

      <!-- Step 2 -->
      <div class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <div class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">2</span>
          <span class="font-bold text-xl text-slate-800">Amount entry</span>
        </div>
        <div class="relative w-full transition-all duration-300 transform group-hover:scale-[1.02]">
          <!-- Card glow effect -->
          <div class="absolute inset-0 bg-gradient-to-br from-slate-100 to-white rounded-2xl shadow-md group-hover:shadow-lg transition-all duration-300"></div>
          
          <!-- Step indicator -->
          <div class="absolute -top-3 -right-3 w-6 h-6 rounded-full bg-gradient-bitcoin flex items-center justify-center text-white text-xs font-bold shadow-md">2</div>
          
          <!-- Widget -->
          <div class="relative p-4">
            <bitcoin-widget
              name="Elon Musk"
              description="Tesla, SpaceX, X"
              image="/path/to/elon.jpg"
              address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
              accent="#000000"
              button-text="Donate bitcoin"
              initial-step="amount"
            />
          </div>
        </div>
      </div>

      <!-- Step 3 -->
      <div class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <div class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">3</span>
          <span class="font-bold text-xl text-slate-800">QR payment</span>
        </div>
        <div class="relative w-full transition-all duration-300 transform group-hover:scale-[1.02]">
          <!-- Card glow effect -->
          <div class="absolute inset-0 bg-gradient-to-br from-slate-100 to-white rounded-2xl shadow-md group-hover:shadow-lg transition-all duration-300"></div>
          
          <!-- Step indicator -->
          <div class="absolute -top-3 -right-3 w-6 h-6 rounded-full bg-gradient-bitcoin flex items-center justify-center text-white text-xs font-bold shadow-md">3</div>
          
          <!-- Widget -->
          <div class="relative p-4">
            <bitcoin-widget
              name="Hal Finney"
              description="Early Bitcoin contributor"
              image="/path/to/hal.jpg"
              address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
              accent="#3B82F6"
              button-text="Donate bitcoin"
              initial-step="qr"
            />
          </div>
        </div>
      </div>

      <!-- Step 4 -->
      <div class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <div class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">4</span>
          <span class="font-bold text-xl text-slate-800">Success</span>
        </div>
        <div class="relative w-full transition-all duration-300 transform group-hover:scale-[1.02]">
          <!-- Card glow effect -->
          <div class="absolute inset-0 bg-gradient-to-br from-slate-100 to-white rounded-2xl shadow-md group-hover:shadow-lg transition-all duration-300"></div>
          
          <!-- Step indicator -->
          <div class="absolute -top-3 -right-3 w-6 h-6 rounded-full bg-gradient-bitcoin flex items-center justify-center text-white text-xs font-bold shadow-md">4</div>
          
          <!-- Widget -->
          <div class="relative p-4">
            <bitcoin-widget
              name="Andreas Antonopoulos"
              description="Bitcoin educator"
              image="/path/to/andreas.jpg"
              address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
              accent="#8B5CF6"
              button-text="Donate bitcoin"
              initial-step="thanks"
            />
          </div>
        </div>
      </div>
    </div>

    <div class="flex justify-center animate-fade-in" style="animation-delay: 0.3s;">
      <Button 
        @click="$router.push('/generate')"
        variant="bitcoin"
        size="lg"
        class="font-medium shadow-md"
      >
        Create your widget
        <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ml-1">
          <path d="M5 12h14"></path>
          <path d="m12 5 7 7-7 7"></path>
        </svg>
      </Button>
    </div>
  </section>
</template>

<script setup>
import { Button } from '@/components/ui/button'
import BitcoinWidget from '@/components/BitcoinWidget.vue'
</script>

<style scoped>
@media (max-width: 767px) {
  .grid {
    grid-template-columns: 1fr;
  }
}
</style>