<template>
  <!-- We need the dark overlay -->
  <!-- Make sure the overlay covers everything -->
  <!-- We need a container for the little window -->
  <div class="overlay">
    <div class="container">
      <Cart :order="order" status="CHECKOUT" @openModal="handleDialog" />
    </div>
  </div>
</template>

<script setup>
import Cart from "./Cart.vue";
const props = defineProps(["order"]);

const emit = defineEmits(["openModal"]);
const handleDialog = () => {
  emit("openModal");
};
</script>

<style scoped>
.overlay {
  background-color: rgba(0, 0, 0, 0.5);
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;

  display: flex;
  justify-content: center;
  align-items: center;

  .container {
    padding: 2rem;
    background-color: white;
    border-radius: 12px;
  }
}
</style>
