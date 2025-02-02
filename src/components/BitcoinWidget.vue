<template>
  <div>
    <bitcoin-widget
      name="Bitcoin Magazine"
      description="News and information in Bitcoin"
      image="https://pbs.twimg.com/profile_images/1444022922377576453/AzvXYXGr_400x400.jpg"
      address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
      accent="#4d4d4d"
      button-text="Donate Bitcoin"
    />
  </div>
</template>

<script>
export default {
  // Tell Vue this is a custom element to prevent warnings
  compilerOptions: {
    isCustomElement: (tag) => tag === "bitcoin-widget",
  },
};
</script>
