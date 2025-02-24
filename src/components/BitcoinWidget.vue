<template>
  <div>
    <bitcoin-widget
      name="Satoshi Nakamoto"
      description="Creator of Bitcoin"
      image="https://cdn.britannica.com/37/238937-050-45D054F6/Bitcoin-inventor-Satoshi-Nakamoto-pictured-on-a-coin.jpg"
      address="bc1qxy2kgdygjrsqtzq2n0yrf2493p83kkfjhx0wlh"
      accent="#5ecfc7"
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
