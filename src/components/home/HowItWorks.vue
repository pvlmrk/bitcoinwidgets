<template>
  <section class="container mx-auto px-6 mb-24 py-6" aria-labelledby="how-it-works-title">
    <div class="text-center max-w-3xl mx-auto mb-16 animate-slide-up">
      <h2 id="how-it-works-title" class="text-[28px] sm:text-[32px] font-bold mb-4 relative inline-block">
        How it works
        <span class="absolute -bottom-2 left-0 h-[4px] w-full bg-gradient-bitcoin rounded-full opacity-50"></span>
      </h2>
      <p class="text-slate-600 text-base sm:text-[18px] mt-6">
        Your widget guides people through 4 stages: profile view, amount entry, QR payment, and success.
      </p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-x-12 gap-y-16 mb-16 max-w-[1000px] mx-auto">
      <article class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <header class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">1</span>
          <h3 class="font-bold text-lg sm:text-xl text-slate-800">Profile view</h3>
        </header>
        <div class="relative w-full">
          <bitcoin-widget
            name="Satoshi Nakamoto"
            description="Creator of Bitcoin"
            image="https://cdn.britannica.com/37/238937-050-45D054F6/Bitcoin-inventor-Satoshi-Nakamoto-pictured-on-a-coin.jpg"
            address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
            accent="#3B82F6"
            button-text="Donate bitcoin"
            initial-step="start"
          />
        </div>
      </article>

      <article class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <header class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">2</span>
          <h3 class="font-bold text-lg sm:text-xl text-slate-800">Amount entry</h3>
        </header>
        <div class="relative w-full">
          <bitcoin-widget
            name="Satoshi Nakamoto"
            description="Creator of Bitcoin"
            image="https://cdn.britannica.com/37/238937-050-45D054F6/Bitcoin-inventor-Satoshi-Nakamoto-pictured-on-a-coin.jpg"
            address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
            accent="#5ECFC7"
            button-text="Donate bitcoin"
            initial-step="amount"
          />
        </div>
      </article>

      <article class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <header class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">3</span>
          <h3 class="font-bold text-lg sm:text-xl text-slate-800">QR payment</h3>
        </header>
        <div class="relative w-full">
          <bitcoin-widget
            name="Satoshi Nakamoto"
            description="Creator of Bitcoin"
            image="https://cdn.britannica.com/37/238937-050-45D054F6/Bitcoin-inventor-Satoshi-Nakamoto-pictured-on-a-coin.jpg"
            address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
            accent="#8B5CF6"
            button-text="Donate bitcoin"
            initial-step="qr"
          />
        </div>
      </article>

      <article class="flex flex-col items-center w-full max-w-[350px] mx-auto group">
        <header class="flex items-center justify-center mb-6">
          <span class="flex items-center justify-center w-10 h-10 bg-gradient-bitcoin text-white rounded-full font-bold shadow-md mr-3">4</span>
          <h3 class="font-bold text-lg sm:text-xl text-slate-800">Success</h3>
        </header>
        <div class="relative w-full">
          <bitcoin-widget
            name="Bitcoin Magazine"
            description="News in Bitcoin"
            image="https://pbs.twimg.com/profile_images/1444022922377576453/AzvXYXGr_400x400.jpg"
            address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
            accent="#303030"
            button-text="Donate bitcoin"
            initial-step="thanks"
          />
        </div>
      </article>
    </div>

    <div class="flex justify-center animate-fade-in" style="animation-delay: 0.3s;">
      <Button 
        @click="handleGenerateClick(); $router.push('/generate')"
        variant="bitcoin"
        size="lg"
        class="font-medium shadow-md"
      >
        Create your widget
        <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="ml-1" aria-hidden="true">
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

const handleGenerateClick = () => {
  window.scrollTo({
    top: 0,
    behavior: 'instant'
  });
}
</script>

<style scoped>
@media (max-width: 767px) {
  .grid {
    grid-template-columns: 1fr;
  }
}
</style>
