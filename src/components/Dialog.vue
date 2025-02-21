<template>
  <div class="overlay">
    <div class="container">
      <slot />
    </div>
  </div>
</template>

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
