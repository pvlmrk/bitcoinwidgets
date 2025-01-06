<template>
    <section class="container mx-auto px-6 mb-24">
      <h2 class="text-[32px] font-bold mb-4">Why us</h2>
      <p class="text-gray-600 text-[16px] max-w-[600px] mb-14">
        Receiving donations has never been easier. All you need to do is design a widget that suits you and copy/paste a simple code snippet.
      </p>
      
      <div class="flex items-start gap-8">
        <div class="w-[200px] h-[200px]">
        </div>
  
        <div class="w-[280px] h-[370px]">
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