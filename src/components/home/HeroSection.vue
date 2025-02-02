<script setup>
import { Button } from '@/components/ui/button'
import BitcoinWidget from '@/components/BitcoinWidget.vue'
</script>

<template>
  <section class="container mx-auto px-6 mb-24">
    <div class="flex items-center justify-between min-h-[600px] gap-10">
      <div class="max-w-[490px] flex flex-col gap-14 w-full md:w-auto">
        <h1 class="text-[46px] md:text-left text-center font-bold leading-[1.15]">
          Start accepting bitcoin donations on your website
        </h1>
        <p class="text-gray-600 text-[16px] md:text-left text-center">
          Create your customized Bitcoin donation widget in seconds and use it on your website.
        </p>
        <Button 
          @click="$router.push('/generate')"
          class="bg-black text-white hover:bg-black/90 rounded-md h-11 w-[140px] md:mx-0 mx-auto"
        >
          Create widget
        </Button>
      </div>

      <div class="w-full flex justify-center md:w-auto">
        <BitcoinWidget/>
      </div>
    </div>
  </section>
</template>

<style scoped>
@media (max-width: 887px) {
  .flex {
    flex-direction: column;
    justify-content: center;
    text-align: center;
  }

  /* Add this to ensure widget container stays centered */
  .w-full.flex.justify-center {
    display: flex;
    justify-content: center;
    align-items: center;
  }
}

/* Optional: you might want to add some spacing between elements when stacked */
@media (max-width: 767px) {
  .flex {
    gap: 3rem;  /* or whatever spacing you prefer */
  }
}
</style>