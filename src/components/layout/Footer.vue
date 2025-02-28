<template>
  <footer class="border-t border-slate-100 py-12">
    <div class="container mx-auto px-6">
      <div class="flex flex-col md:flex-row justify-between items-center gap-6">
        <RouterLink 
          :to="{path: '/', hash: ''}" 
          class="group font-inter font-bold text-xl sm:text-2xl flex items-center relative overflow-hidden"
          @click="handleClick"
          aria-label="Back to homepage"
        >
          <span class="flex items-center">
            <span class="text-bitcoin-orange" aria-hidden="true">₿</span>itcoin <span class="text-slate-800">Widgets</span>
          </span>
          <span class="absolute bottom-0 left-0 h-[2px] w-0 bg-gradient-bitcoin group-hover:w-full transition-all duration-300" aria-hidden="true"></span>
        </RouterLink>

        <p class="text-slate-500 text-sm">
          © {{ new Date().getFullYear() }} Bitcoin Widgets
        </p>
      </div>
    </div>
  </footer>
</template>

<script setup>
const handleClick = () => {
  window.scrollTo({
    top: 0,
    behavior: 'instant'
  });
}
</script>