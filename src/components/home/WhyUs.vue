<script setup>
import { Button } from "@/components/ui/button";
import BitcoinWidget from "@/components/BitcoinWidget.vue";

const handleGenerateClick = () => {
  window.scrollTo({
    top: 0,
    behavior: "instant",
  });
};
</script>

<template>
  <section
    class="container mx-auto px-6 py-16 mb-28 relative overflow-hidden"
    aria-labelledby="why-us-title"
  >
    <div
      class="absolute inset-0 bg-gradient-to-b from-white via-slate-50/50 to-white pointer-events-none"
    ></div>
    <div class="absolute inset-0 opacity-5 pointer-events-none">
      <svg
        width="100%"
        height="100%"
        xmlns="http://www.w3.org/2000/svg"
        aria-hidden="true"
      >
        <defs>
          <pattern
            id="btcGrid"
            x="0"
            y="0"
            width="20"
            height="20"
            patternUnits="userSpaceOnUse"
          >
            <path
              d="M10,0 L20,10 L10,20 L0,10 Z"
              fill="none"
              stroke="#F7931A"
              stroke-width="0.5"
            />
          </pattern>
        </defs>
        <rect width="100%" height="100%" fill="url(#btcGrid)" />
      </svg>
    </div>

    <div class="relative">
      <div class="text-center max-w-3xl mx-auto mb-16 animate-slide-up">
        <h2
          id="why-us-title"
          class="text-[28px] sm:text-[32px] font-bold mb-4 relative inline-block"
        >
          Why us
          <span
            class="absolute -bottom-2 left-0 h-[4px] w-full bg-gradient-bitcoin rounded-full opacity-50"
          ></span>
        </h2>
        <p class="text-slate-600 text-base sm:text-[18px] mt-6">
          Upgrade your static Bitcoin QR code to an interactive widget that
          catches the eye with customizable design.
        </p>
      </div>

      <div class="flex flex-col md:flex-row items-center justify-evenly mb-28">
        <article class="flex flex-col gap-6 items-center md:w-[350px]">
          <header class="flex items-center gap-2 mb-2">
            <span
              class="text-red-500 text-lg sm:text-xl font-bold"
              aria-hidden="true"
              >❌</span
            >
            <h3 class="font-bold text-lg sm:text-xl">Before</h3>
          </header>

          <div class="relative group">
            <div
              class="absolute inset-0 rounded-xl bg-white border border-slate-200 shadow-md transform transition-transform duration-300 group-hover:rotate-2 dark:bg-slate-200"
            ></div>

            <div
              class="relative p-4 rounded-xl overflow-hidden bg-white border border-slate-200 shadow-md group-hover:shadow-lg transition-all duration-300 dark:bg-slate-200"
            >
              <div
                class="w-full h-[320px] rounded-lg flex flex-col items-center justify-center gap-4"
              >
                <div class="text-center"></div>

                <img
                  src="/src/assets/qr-code.png"
                  alt="Static QR Code Example"
                  class="w-full h-full object-contain"
                />
              </div>
            </div>
          </div>
        </article>

        <div
          class="hidden md:flex items-center justify-center"
          aria-hidden="true"
        >
          <div class="relative w-24 h-24">
            <div class="absolute inset-0 flex items-center justify-center">
              <svg
                xmlns="http://www.w3.org/2000/svg"
                width="48"
                height="48"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
                class="text-bitcoin-orange"
              >
                <line x1="5" y1="12" x2="19" y2="12"></line>
                <polyline points="12 5 19 12 12 19"></polyline>
              </svg>
            </div>
            <div
              class="absolute inset-0 rounded-full border-4 border-bitcoin-orange border-dashed animate-spin-slow opacity-20"
            ></div>
          </div>
        </div>

        <article class="flex flex-col gap-6 items-center md:w-[350px]">
          <header class="flex items-center gap-2 mb-2">
            <span
              class="text-green-500 text-lg sm:text-xl font-bold"
              aria-hidden="true"
              >✅</span
            >
            <h3 class="font-bold text-lg sm:text-xl">After</h3>
          </header>

          <div class="relative group">
            <div
              class="absolute -inset-1 bg-gradient-to-r from-bitcoin-orange/20 to-bitcoin-light/20 rounded-xl blur opacity-0 group-hover:opacity-100 transition-opacity duration-500"
            ></div>

            <div class="relative">
              <bitcoin-widget
                name="Michael Saylor"
                description="Strategy CEO"
                image="https://pbs.twimg.com/profile_images/1485632175932383235/8t0DGo6V_400x400.jpg"
                address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
                accent="#c13634"
                button-text="Donate bitcoin"
              />
            </div>
          </div>
        </article>
      </div>

      <section aria-labelledby="feature-comparison-title">
        <h3
          id="feature-comparison-title"
          class="text-lg sm:text-xl font-bold mb-6 text-center dark:text-white"
        >
          Compare the difference
        </h3>

        <div
          class="grid grid-cols-1 md:grid-cols-3 gap-6 max-w-[90%] mx-auto mb-16"
        >
          <article
            class="group bg-white dark:bg-slate-700 rounded-xl p-5 shadow-sm hover:shadow-lg dark:hover:shadow-slate-900 transition-all duration-300 ease-in-out border border-slate-100 dark:border-slate-600 hover:border-orange-100 dark:hover:border-orange-500"
          >
            <div class="flex items-start">
              <div
                class="flex-shrink-0 p-2 rounded-lg bg-orange-50 dark:bg-orange-900/30 group-hover:bg-orange-100 dark:group-hover:bg-orange-800/40 transition-colors duration-300 mr-3.5"
                aria-hidden="true"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="text-orange-500 dark:text-orange-400 group-hover:text-orange-600 dark:group-hover:text-orange-300 transition-colors duration-300"
                >
                  <path
                    d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10z"
                  ></path>
                  <path d="m7 12 3 3 7-7"></path>
                </svg>
              </div>
              <div>
                <h4
                  class="font-medium text-slate-800 dark:text-slate-100 mb-1 group-hover:text-slate-900 dark:group-hover:text-white transition-colors duration-300"
                >
                  Interactive
                </h4>
                <p
                  class="text-slate-600 dark:text-slate-300 text-sm group-hover:text-slate-700 dark:group-hover:text-slate-200 transition-colors duration-300"
                >
                  Multi-step process guides users through the donation flow
                </p>
              </div>
            </div>
          </article>

          <article
            class="group bg-white dark:bg-slate-700 rounded-xl p-5 shadow-sm hover:shadow-lg dark:hover:shadow-slate-900 transition-all duration-300 ease-in-out border border-slate-100 dark:border-slate-600 hover:border-orange-100 dark:hover:border-orange-500"
          >
            <div class="flex items-start">
              <div
                class="flex-shrink-0 p-2 rounded-lg bg-orange-50 dark:bg-orange-900/30 group-hover:bg-orange-100 dark:group-hover:bg-orange-800/40 transition-colors duration-300 mr-3.5"
                aria-hidden="true"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="text-orange-500 dark:text-orange-400 group-hover:text-orange-600 dark:group-hover:text-orange-300 transition-colors duration-300"
                >
                  <path
                    d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10z"
                  ></path>
                  <path d="m7 12 3 3 7-7"></path>
                </svg>
              </div>
              <div>
                <h4
                  class="font-medium text-slate-800 dark:text-slate-100 mb-1 group-hover:text-slate-900 dark:group-hover:text-white transition-colors duration-300"
                >
                  Customizable
                </h4>
                <p
                  class="text-slate-600 dark:text-slate-300 text-sm group-hover:text-slate-700 dark:group-hover:text-slate-200 transition-colors duration-300"
                >
                  Personalize with your colors, image, and profile details
                </p>
              </div>
            </div>
          </article>

          <article
            class="group bg-white dark:bg-slate-700 rounded-xl p-5 shadow-sm hover:shadow-lg dark:hover:shadow-slate-900 transition-all duration-300 ease-in-out border border-slate-100 dark:border-slate-600 hover:border-orange-100 dark:hover:border-orange-500"
          >
            <div class="flex items-start">
              <div
                class="flex-shrink-0 p-2 rounded-lg bg-orange-50 dark:bg-orange-900/30 group-hover:bg-orange-100 dark:group-hover:bg-orange-800/40 transition-colors duration-300 mr-3.5"
                aria-hidden="true"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="18"
                  height="18"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2.5"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="text-orange-500 dark:text-orange-400 group-hover:text-orange-600 dark:group-hover:text-orange-300 transition-colors duration-300"
                >
                  <path
                    d="M12 22c5.523 0 10-4.477 10-10S17.523 2 12 2 2 6.477 2 12s4.477 10 10 10z"
                  ></path>
                  <path d="m7 12 3 3 7-7"></path>
                </svg>
              </div>
              <div>
                <h4
                  class="font-medium text-slate-800 dark:text-slate-100 mb-1 group-hover:text-slate-900 dark:group-hover:text-white transition-colors duration-300"
                >
                  Professional
                </h4>
                <p
                  class="text-slate-600 dark:text-slate-300 text-sm group-hover:text-slate-700 dark:group-hover:text-slate-200 transition-colors duration-300"
                >
                  Stands out with a polished, modern design that inspires trust
                </p>
              </div>
            </div>
          </article>
        </div>
      </section>

      <div
        class="flex justify-center animate-fade-in"
        style="animation-delay: 0.3s"
      >
        <Button
          @click="
            handleGenerateClick();
            $router.push('/generate');
          "
          variant="bitcoin"
          size="lg"
          class="font-medium shadow-md"
        >
          Create your widget
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
            class="ml-1"
            aria-hidden="true"
          >
            <path d="M5 12h14"></path>
            <path d="m12 5 7 7-7 7"></path>
          </svg>
        </Button>
      </div>
    </div>
  </section>
</template>

<style scoped>
@media (max-width: 767px) {
  .flex-col.md\:flex-row {
    gap: 4rem;
  }
}
</style>
