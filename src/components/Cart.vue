<!-- Here goes the HTML kind of a thing -->
<template>
  <div class="cart">
    <h2 class="title">Your Cart ({{ totalItems() }})</h2>
    <ul>
      <li v-for="item in props.order">
        <div>
          <span class="name">{{ item.name }}</span>
          <div class="info">
            <span class="quantity">{{ item.quantity }}x</span>
            <span class="price">@ ${{ item.price }}</span>
            <span class="total">${{ item.price * item.quantity }}</span>
          </div>
        </div>
        <img src="/public/assets/images/icon-remove-item.svg" />
      </li>
    </ul>
    <div class="order-total">
      <span>Order total</span>
      <h2>${{ totalCost() }}</h2>
    </div>

    <button class="confirm-order">Confirm Order</button>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps(["order"]);

// For future... remember this might become a computed
const totalItems = () => {
  let total = 0;

  for (const item of props.order) {
    total = total + item.quantity;
  }

  return total;
};

const totalCost = () => {
  let total = 0;

  for (const item of props.order) {
    total = total + item.quantity * item.price;
  }

  return total.toFixed(2);
};
</script>

<style scoped>
.cart {
  background-color: white;
  border-radius: 12px;
  padding: 24px;

  .title {
    color: #c73b0f;
  }

  ul {
    li {
      font-size: 14px;
      font-weight: normal;
      list-style: none;
      padding: 16px 0;
      border-bottom: 1px solid #f5eeec;
      display: flex;
      justify-content: space-between;
      align-items: center;

      .name,
      .quantity,
      .total {
        font-weight: 600; /* semibold */
      }
      .quantity {
        color: #c73b0f;
      }
      .info {
        margin-top: 8px;
        display: flex;
        gap: 8px;
      }

      img {
        border: 1px solid #ad8a85;
        border-radius: 50%;
        padding: 2px;
      }
    }
  }

  .order-total {
    display: flex;
    justify-content: space-between;
    margin-top: 24px;
  }

  .confirm-order {
    /* change the background color */
    background-color: #c73b0f;
    /* change the text color */
    color: white;
    /* change the vertical padding to 16px */
    padding: 16px 0;
    /* change the width */
    width: 100%;
    /* add round edges */
    border-radius: 32px;
    /* 24px top margin */
    margin-top: 24px;
    /* removed borders */
    border-style: none;
  }
}
</style>
