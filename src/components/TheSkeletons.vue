<script setup lang="ts"></script>

<template>
  <div class="big-line"></div>
  <div class="med-line-container">
    <div class="med-line"></div>
    <div class="med-line"></div>
    <div class="med-line"></div>
  </div>
  <div class="smaller-line"></div>
  <div class="smallest-line"></div>
</template>

<style scoped>
.big-line {
  width: 211px;
  height: 30px;
  border-radius: 8px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444 51.04%, #333 100%);
}

.med-line-container {
  margin-top: 24px;
  display: flex;
  width: 211px;
  flex-direction: column;
  align-items: flex-start;
  gap: 16px;
  border-radius: 4px;
  margin-bottom: 16px;
}

.med-line {
  height: 10px;
  border-radius: 4px;
  width: 100%;
  background: linear-gradient(90deg, #3c3c3c 0%, #444 51.04%, #333 100%);
}

.smaller-line {
  width: 180px;
  height: 10px;
  flex-shrink: 0;
  border-radius: 4px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444 51.04%, #333 100%);
  margin-bottom: 16px;
}

.smallest-line {
  width: 80px;
  height: 10px;
  flex-shrink: 0;
  border-radius: 4px;
  background: linear-gradient(90deg, #3c3c3c 0%, #444 51.04%, #333 100%);
  margin-bottom: 24px;
}
</style>
