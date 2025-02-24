<script setup>
import { Button } from '@/components/ui/button'
import BitcoinWidget from '@/components/BitcoinWidget.vue'
</script>

<template>
  <section class="container mx-auto px-6 py-16 mb-24 relative overflow-hidden">
    <!-- Background pattern -->
    <div class="absolute inset-0 bg-gradient-to-b from-white via-slate-50/50 to-white pointer-events-none"></div>
    <div class="absolute inset-0 opacity-5 pointer-events-none">
      <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <pattern id="btcGrid" x="0" y="0" width="20" height="20" patternUnits="userSpaceOnUse">
            <path d="M10,0 L20,10 L10,20 L0,10 Z" fill="none" stroke="#F7931A" stroke-width="0.5"/>
          </pattern>
        </defs>
        <rect width="100%" height="100%" fill="url(#btcGrid)" />
      </svg>
    </div>
    
    <div class="relative">
      <div class="text-center max-w-3xl mx-auto mb-16 animate-slide-up">
        <h2 class="text-[32px] font-bold mb-4 relative inline-block">
          Why us
          <span class="absolute -bottom-2 left-0 h-[4px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
        </h2>
        <p class="text-slate-600 text-[18px] mt-6">
          Upgrade your static Bitcoin QR code to an interactive widget that catches the eye with customizable design.
        </p>
      </div>
      
      <div class="flex flex-col md:flex-row items-center justify-center gap-12 mb-24">
        <div class="flex flex-col gap-6 items-center md:w-[350px]">
          <div class="flex items-center gap-2 mb-2">
            <span class="text-red-500 text-xl font-bold">❌</span>
            <span class="font-bold text-xl">Before</span>
          </div>
          
          <div class="relative group">
            <!-- Card background -->
            <div class="absolute inset-0 rounded-xl bg-white border border-slate-200 shadow-md transform transition-transform duration-300 group-hover:rotate-2"></div>
            
            <!-- Card content -->
            <div class="relative p-4 rounded-xl overflow-hidden bg-white border border-slate-200 shadow-md group-hover:shadow-lg transition-all duration-300">
              <div class="w-full h-[320px] rounded-lg flex flex-col items-center justify-center gap-4">
                <div class="text-center">
                </div>
                
                <img src="/src/assets/qr-code.png" alt="Static QR Code" class="w-full h-full object-contain" />
                
              </div>
            </div>
          </div>
        </div>

        <div class="hidden md:flex items-center justify-center">
          <div class="relative w-24 h-24">
            <div class="absolute inset-0 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-bitcoin-orange">
                <line x1="5" y1="12" x2="19" y2="12"></line>
                <polyline points="12 5 19 12 12 19"></polyline>
              </svg>
            </div>
            <div class="absolute inset-0 rounded-full border-4 border-bitcoin-orange border-dashed animate-spin-slow opacity-20"></div>
          </div>
        </div>

        <div class="flex flex-col gap-6 items-center md:w-[350px]">
          <div class="flex items-center gap-2 mb-2">
            <span class="text-green-500 text-xl font-bold">✅</span>
            <span class="font-bold text-xl">After</span>
          </div>
          
          <div class="relative group">
            <!-- Glow effect -->
            <div class="absolute -inset-1 bg-gradient-to-r from-bitcoin-orange/20 to-bitcoin-light/20 rounded-xl blur opacity-0 group-hover:opacity-100 transition-opacity duration-500"></div>
            
            <!-- Widget container -->
            <div class="relative">
              <BitcoinWidget
                name="Elon Musk"
                description="Tesla, SpaceX, X"
                image="/path/to/elon.jpg"
                :accent="'#000000'"
              />
            </div>
          </div>
        </div>
      </div>
      
      <!-- Feature comparison -->
      <div class="max-w-[900px] mx-auto mb-16 bg-white rounded-xl p-8 shadow-md">
        <h3 class="text-xl font-bold mb-6 text-center">Compare the difference</h3>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="bg-slate-50 rounded-lg p-6 hover:shadow-md transition-shadow duration-300">
            <div class="flex items-center mb-3">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-bitcoin-orange mr-2">
                <path d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10z"></path>
                <path d="m7 12 3 3 7-7"></path>
              </svg>
              <h4 class="font-medium">Interactive</h4>
            </div>
            <p class="text-slate-600 text-sm">
              Multi-step process guides users through the donation flow
            </p>
          </div>
          
          <div class="bg-slate-50 rounded-lg p-6 hover:shadow-md transition-shadow duration-300">
            <div class="flex items-center mb-3">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-bitcoin-orange mr-2">
                <path d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10z"></path>
                <path d="m7 12 3 3 7-7"></path>
              </svg>
              <h4 class="font-medium">Customizable</h4>
            </div>
            <p class="text-slate-600 text-sm">
              Personalize with your colors, image, and profile details
            </p>
          </div>
          
          <div class="bg-slate-50 rounded-lg p-6 hover:shadow-md transition-shadow duration-300">
            <div class="flex items-center mb-3">
              <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-bitcoin-orange mr-2">
                <path d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10z"></path>
                <path d="m7 12 3 3 7-7"></path>
              </svg>
              <h4 class="font-medium">Professional</h4>
            </div>
            <p class="text-slate-600 text-sm">
              Stands out with a polished, modern design that inspires trust
            </p>
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
    </div>
  </section>
</template>

<style scoped>
@media (max-width: 767px) {
  .flex-col.md\:flex-row {
    gap: 4rem;
  }
}
</style>