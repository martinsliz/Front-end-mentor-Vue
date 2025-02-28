<template>
  <div class="image-container">
    <img class="product-image" :src="props.image" alt="Waffle image" />

    <button
      @click="dummyFunction"
      class="add-to-cart"
      :class="{ 'add-to-cart-active': props.quantity > 0 }"
    >
      <span v-if="props.quantity === 0">Add to Cart</span>
      <span v-else>{{ props.quantity }}</span>
    </button>
  </div>
  <p class="category">{{ props.category }}</p>
  <p class="name">{{ props.name }}</p>
  <p class="price">${{ props.price }}</p>
</template>

<script setup>
// We need to make this component aware
// of the existance of props being passed down

const props = defineProps(["name", "price", "category", "image", "quantity"]);
const emit = defineEmits(["uptCartEvent"]);

const dummyFunction = () => {
  const payload = {
    name: props.name,
    price: props.price,
    quantity: 1,
  };

  emit("uptCartEvent", payload);
};
</script>

<style scoped>
.image-container {
  display: flex;
  flex-direction: column;
  align-items: center;

  .product-image {
    width: 100%;
    z-index: -1;
  }

  .add-to-cart {
    width: 160px;
    height: 40px;
    border-radius: 20px;
    background-color: white;
    border: 1px solid gray;
    margin-top: -20px;
  }

  .add-to-cart-active {
    background-color: #c73b0f;
    color: white;
    border: none;
  }
}

.category {
  color: gray;
  margin-bottom: 8px;
}

.name {
  color: black;
  font-weight: bold;
  margin-bottom: 8px;
}

.price {
  color: hsl(14, 86%, 42%);
  font-weight: bold;
  margin-bottom: 8px;
}
</style>
