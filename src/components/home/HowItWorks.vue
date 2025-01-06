<template>
    <section class="container mx-auto px-6 mb-24">
      <h2 class="text-[32px] font-bold mb-4">How it works</h2>
      <p class="text-gray-600 text-[16px] max-w-[600px] mb-14">
        You can start accepting bitcoin donations through a bitcoin payment processor right away. Just generate a widget, integrate it, and you're ready.
      </p>
  
      <div class="grid grid-cols-2 gap-8">
        <div class="h-[220px]">
        </div>
  
        <div class="h-[220px]">
        </div>
  
        <div class="h-[220px]">
        </div>
  
        <div class="h-[220px]">
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
  </script>