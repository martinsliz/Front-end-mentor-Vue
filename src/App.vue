<script setup>
import Product from "./components/Product.vue";
import Cart from "./components/Cart.vue";
import Dialog from "./components/Dialog.vue";

import jsonDataArray from "../public/data.json";
import { ref } from "vue";

const order = ref([]);

// This is going to be used to show and hide the dialog modal
const showDialog = ref(false);

const handleDialog = () => {
  console.log("Received openModal event");
  showDialog.value = !showDialog.value;
};

const handleCart = (payload) => {
  // Look if the item is already in the cart
  const alreadyInCart = order.value.findIndex((item) => {
    console.log("Comparing ", item.name, " with ", payload.name);
    return item.name === payload.name;
  });

  if (alreadyInCart >= 0) {
    // If yes, increase quantity
    order.value[alreadyInCart].quantity++;
  } else {
    // If not add it (with push)
    order.value.push(payload);
  }
};
</script>

<template>
  <main>
    <Cart :order="order" status="PENDING" @openModal="handleDialog" />

    <h1>Desserts</h1>

    <Product
      v-for="tempProduct in jsonDataArray"
      :name="tempProduct.name"
      :price="tempProduct.price"
      :category="tempProduct.category"
      :image="tempProduct.image.mobile"
      @uptCartEvent="handleCart"
    />
  </main>
  <Dialog v-if="showDialog" :order="order" @openModal="handleDialog" />
</template>

<style scoped>
main {
  padding: 25px;

  h1 {
    margin-bottom: 20px;
  }
}
</style>
