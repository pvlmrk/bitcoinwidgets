<script setup>
import { Button } from '@/components/ui/button'
import BitcoinWidget from '@/components/BitcoinWidget.vue'
</script>
<template>
  <section class="container mx-auto px-6 mb-24">
    <h2 class="text-[32px] font-bold mb-4">Why us</h2>
    <p class="text-gray-600 text-[16px] mb-14">
      Upgrade your static Bitcoin QR code to an interactive widget that catches the eye with customizable design.
    </p>
    
    <div class="flex items-start justify-evenly mb-14 min-w-0"> <!-- Added min-w-0 to prevent overflow -->
      <div class="flex flex-col gap-2 items-center w-[350px]">
        <span class="text-red-500 text-xl font-bold">❌ Before</span>
        <div class="w-full h-[343px] rounded-lg bg-white border border-gray-200 shadow-lg flex items-center justify-center hover:bg-gray-100 hover:cursor-pointer ease-in-out transition-all duration-300">
          <img src="/src/assets/qr-code.png" alt="Static QR Code" class="w-[280px] h-[280px] object-contain" />
        </div>
      </div>

      <div class="flex flex-col gap-2 items-center">
        <span class="text-green-500 text-xl font-bold">✅ After</span>
        <BitcoinWidget
          name="Elon Musk"
          description="Tesla, SpaceX, X"
          image="/elon-profile.jpg"
          :accent="'#000000'"
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

<style scoped>
@media (max-width: 767px) {
  .flex.items-start {
    flex-direction: column;
    align-items: center;
    gap: 4rem;
  }

  h2, p {
    text-align: center;
  }
 
  /* Make paragraph width full and center it */
  p {
    max-width: 100%;
    margin-left: auto;
    margin-right: auto;
  }
}
</style>