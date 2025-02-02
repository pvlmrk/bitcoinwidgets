<template>
  <section class="container mx-auto px-6 mb-24">
    <h2 class="text-[32px] font-bold mb-4">How it works</h2>
    <p class="text-gray-600 text-[16px] mb-14">
      Your widget guides people through 4 stages: profile view, amount entry, QR payment, and success.
    </p>

    <div class="grid grid-cols-2 gap-x-12 gap-y-12 mb-14 max-w-[900px] mx-auto">
      <div class="flex flex-col items-center w-[350px] mx-auto">
        <span class="font-bold text-lg mb-4">1. Profile view</span>
        <bitcoin-widget
          name="Bitcoin Magazine"
          description="News and information in Bitcoin"
          image="https://pbs.twimg.com/profile_images/1444022922377576453/AzvXYXGr_400x400.jpg"
          address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
          accent="#E5A15E"
          button-text="Donate Bitcoin"
          initial-step="start"
        />
      </div>

      <div class="flex flex-col items-center w-[350px] mx-auto">
        <span class="font-bold text-lg mb-4">2. Amount entry</span>
        <bitcoin-widget
          name="Bitcoin Magazine"
          description="News and information in Bitcoin"
          image="https://pbs.twimg.com/profile_images/1444022922377576453/AzvXYXGr_400x400.jpg"
          address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
          accent="#E5A15E"
          button-text="Donate Bitcoin"
          initial-step="amount"
        />
      </div>

      <div class="flex flex-col items-center w-[350px] mx-auto">
        <span class="font-bold text-lg mb-4">3. QR payment</span>
        <bitcoin-widget
          name="Bitcoin Magazine"
          description="News and information in Bitcoin"
          image="https://pbs.twimg.com/profile_images/1444022922377576453/AzvXYXGr_400x400.jpg"
          address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
          accent="#E5A15E"
          button-text="Donate Bitcoin"
          initial-step="qr"
        />
      </div>

      <div class="flex flex-col items-center w-[350px] mx-auto">
        <span class="font-bold text-lg mb-4">4. Success</span>
        <bitcoin-widget
          name="Bitcoin Magazine"
          description="News and information in Bitcoin"
          image="https://pbs.twimg.com/profile_images/1444022922377576453/AzvXYXGr_400x400.jpg"
          address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
          accent="#E5A15E"
          button-text="Donate Bitcoin"
          initial-step="thanks"
        />
      </div>
    </div>

    <div class="flex justify-center">
      <Button 
        @click="$router.push('/generate')"
        class="h-11 bg-black text-white hover:bg-black/90"
      >
        Create widget
      </Button>
    </div>
  </section>
</template>

<script setup>
import { Button } from '@/components/ui/button'
import BitcoinWidget from '@/components/BitcoinWidget.vue'
</script>

<style scoped>
@media (max-width: 887px) {
  .grid {
    grid-template-columns: 1fr;
  }

  h2, p {
    text-align: center;
  }

  p {
    max-width: 100%;
    margin-left: auto;
    margin-right: auto;
  }
}
</style>