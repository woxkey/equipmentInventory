<script setup lang="ts">
import TheSkeletons from "./TheSkeletons.vue";
</script>

<template>
  <div class="container">
    <img src="../assets/mainImg.png" alt="#" />
    <TheSkeletons />
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  width: 236px;
  padding: 18px 14px 24px 14px;
  flex-direction: column;
  align-items: center;
  height: 500px;
  border-radius: 12px;
  border: 1px solid #4d4d4d;
  background: var(--seondary-bg, #262626);
  box-sizing: border-box;
  margin-right: 24px;

  img {
    margin-bottom: 20px;
  }
}
</style>
