<script setup>
import { Button } from '@/components/ui/button'
import BitcoinWidget from '@/components/BitcoinWidget.vue'
</script>

<template>
  <section class="container mx-auto px-6 mb-24 pt-8">
    <div class="flex flex-col md:flex-row items-center justify-between min-h-[600px] gap-10">
      <!-- Left content -->
      <div class="max-w-[490px] flex flex-col gap-14 w-full md:w-auto animate-slide-up">
        <h1 class="text-[46px] md:text-left text-center font-bold leading-[1.15] text-slate-900 relative">
          <span class="text-bitcoin-orange">₿</span>itcoin donations
          <span class="relative">
            made simple
            <span class="absolute -bottom-2 left-0 h-[6px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
          </span>
        </h1>
        <p class="text-slate-700 text-[18px] md:text-left text-center leading-relaxed">
          Create your customized Bitcoin donation widget in seconds and enhance your website with a professional, interactive payment solution.
        </p>
        <Button 
          @click="$router.push('/generate')"
          variant="bitcoin" 
          size="lg"
          class="w-[180px] md:mx-0 mx-auto font-medium"
        >
          Create widget
          <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ml-1">
            <path d="M5 12h14"></path>
            <path d="m12 5 7 7-7 7"></path>
          </svg>
        </Button>
      </div>

      <!-- Right widget -->
      <div class="w-full flex justify-center items-center md:w-auto">
        <div class="relative p-8 animate-fade-in">
          <!-- Glow effect -->
          <div class="absolute inset-0 bg-gradient-to-r from-bitcoin-orange/5 to-bitcoin-light/10 rounded-3xl blur-xl animate-pulse-gentle"></div>
          
          <!-- Background pattern -->
          <div class="absolute inset-0 overflow-hidden rounded-3xl opacity-10">
            <svg width="100%" height="100%" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
              <defs>
                <pattern id="btcPattern" patternUnits="userSpaceOnUse" width="10" height="10">
                  <path d="M5,2.5 L7.5,5 L5,7.5 L2.5,5 Z" fill="currentColor" class="text-bitcoin-orange"/>
                </pattern>
              </defs>
              <rect width="100%" height="100%" fill="url(#btcPattern)" />
            </svg>
          </div>
          
          <!-- Widget -->
          <div class="relative z-10 transform hover:scale-[1.02] transition-transform duration-300">
            <BitcoinWidget
              name="Bitcoin Widgets"
              description="Interactive payment solution for your site"
              accent="#F7931A"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
@media (max-width: 767px) {
  .flex-col.md\:flex-row {
    gap: 3rem;
  }
}
</style>