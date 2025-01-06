<script setup>
import { Button } from '@/components/ui/button'
</script>

<template>
  <section class="container mx-auto px-6 mb-24">
    <div class="flex items-center justify-between h-[600px]">
      <div class="max-w-[490px] flex flex-col gap-14">
        <h1 class="text-[46px] font-bold leading-[1.15]">
          Start accepting bitcoin donations on your website
        </h1>
        <p class="text-gray-600 text-[16px]">
          Create your customized Bitcoin donation widget in seconds and use it on your website.
        </p>
        <Button 
          @click="$router.push('/generate')"
          class="bg-black text-white hover:bg-black/90 rounded-md h-11 w-[140px]"
        >
          Create widget
        </Button>
      </div>

      <div class="w-[350px] h-[370px]">
      </div>
    </div>
  </section>
</template>