<template>
  <div class="icon" @click="updateParentValue">
    <svg
      width="24"
      height="24"
      viewBox="0 0 24 24"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <g id="carbon:close">
        <path
          id="Vector"
          d="M18 7.05L16.95 6L12 10.95L7.05 6L6 7.05L10.95 12L6 16.95L7.05 18L12 13.05L16.95 18L18 16.95L13.05 12L18 7.05Z"
          fill="white"
        />
      </g>
    </svg>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  showValue: Boolean,
});
const emit = defineEmits(["updateValue"]);

const updateParentValue = () => {
  const newValue: boolean = !props.showValue;
  emit("updateValue", newValue);
};
</script>

<style scoped>
.icon {
  margin-bottom: 20px;
  text-align: end;
  width: 100%;
  cursor: pointer;
}
</style>
