<template>
    <div class="w-auto p-0">
      <input
        type="color"
        v-model="selectedColor"
        class="w-12 h-10 cursor-pointer border-0 rounded-md p-1"
      />
    </div>
  </template>
  
  <script>
  export default {
    name: "ColorPicker",
    data() {
      return {
        selectedColor: "#F7931A"
      };
    }
  };
  </script>
  
  <style scoped>
  input[type="color"] {
    -webkit-appearance: none;
    appearance: none;
    background-color: #e6eaee;
  }
  </style>
  