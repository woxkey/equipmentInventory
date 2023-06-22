<script setup lang="ts">
</script>

<template>
  <div class="container">
    <div class="line"></div>
    <img src="../assets/closeBtn.svg" alt="close" />
  </div>
</template>

<style scoped>
.container {
  width: 760px;
  height: 72px;
  flex-shrink: 0;
  border-radius: 12px;
  border: 1px solid #4d4d4d;
  background: #262626;
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
.line {
  margin-left: 18px;
  width: 699px;
  height: 36px;
  flex-shrink: 0;
  border-radius: 12px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444 51.04%, #333 100%);
}
img {
  align-self: flex-start;
  width: 24px;
  height: 24px;
  flex-shrink: 0;
  padding-top: 8px;
  padding-right: 8px;
  cursor: pointer;
}
</style>
