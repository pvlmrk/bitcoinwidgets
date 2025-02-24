<template>
  <footer class="bg-slate-50 border-t border-slate-100 py-20">
    <div class="container mx-auto px-6">
      <!-- Simple flex layout footer -->
      <div class="flex flex-col md:flex-row justify-between items-center gap-6">
        <!-- Logo - flex start -->
        <RouterLink to="/" class="group font-inter font-bold text-2xl flex items-center relative overflow-hidden">
          <span class="flex items-center">
            <span class="text-bitcoin-orange">₿</span>itcoin <span class="text-slate-800">Widgets</span>
          </span>
          <span class="absolute bottom-0 left-0 h-[2px] w-0 bg-gradient-bitcoin group-hover:w-full transition-all duration-300"></span>
        </RouterLink>

        <!-- Copyright - flex end -->
        <p class="text-slate-500 text-sm">
          © {{ new Date().getFullYear() }} Bitcoin Widgets
        </p>
      </div>
    </div>
  </footer>
</template>