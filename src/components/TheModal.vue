<script lang="ts" setup>
import IconGreenFolderVue from "./icons/IconGreenFolder.vue";
import IconBlueFolderVue from "./icons/IconBlueFolder.vue";
import IconYellowFolderVue from "./icons/IconYellowFolder.vue";
import IconClose from "./icons/IconCloseBtn.vue";
import { ref, watch } from "vue";
import type { Item } from "./TheInventory.vue";
import TheSkeletons from "./TheSkeletons.vue";

const props = defineProps({
  myShow: Boolean,
  updateValue: Function,
  selectedItemId: Number,
  items: { type: Array as () => Item[], required: true },
  selectedType: String,
});

watch(
  () => props.myShow,
  (newValue) => {
    if (newValue) {
      isDeleting.value = false;
    }
  }
);

const isDeleting = ref(false);
const numberOfItemsToDelete = ref("");

const handleDelete = () => {
  const copyItems = ref<Item[]>(props.items);
  const item = copyItems.value.find((item) => item.id === props.selectedItemId);
  if (item) {
    const itemsCount = Math.abs(parseInt(numberOfItemsToDelete.value));
    item.items = item.items - itemsCount >= 0 ? item.items - itemsCount : 0;
  }
  isDeleting.value = false;
  numberOfItemsToDelete.value = "";
};
</script>

<template>
  <transition name="modal" :appear="true">
    <div class="modal" v-if="props.myShow">
      <IconClose :showValue="props.myShow" @updateValue="props.updateValue" />
      <IconGreenFolderVue v-if="selectedType === 'green'" class="myIcon" />
      <IconBlueFolderVue v-else-if="selectedType === 'blue'" class="myIcon" />
      <IconYellowFolderVue v-else class="myIcon" />

      <div class="modal__lineFirst"></div>
      <TheSkeletons />
      <div class="line"></div>
      <button
        v-if="!isDeleting"
        @click="isDeleting = true"
        class="modal-deleteBtn"
      >
        Удалить предмет
      </button>
      <div class="cancelConfirm-container" v-else>
        <input
          v-model="numberOfItemsToDelete"
          min="0"
          placeholder="Введите количество"
          class="modal-input"
          type="number"
        />
        <div class="buttons-inner">
          <button @click="isDeleting = false" class="buttons-inner__cancelBtn">
            Отмена
          </button>
          <button
            :disabled="numberOfItemsToDelete ? false : true"
            @click="handleDelete"
            class="buttons-inner__confirmBtn"
          >
            Подтвердить
          </button>
        </div>
      </div>
    </div>
  </transition>
</template>

<style scoped lang="scss">
.modal {
  position: absolute;
  right: 0;
  top: 0;
  width: 250px;
  height: 500px;
  background: rgba(38, 38, 38, 0.5);
  backdrop-filter: blur(8px);
  z-index: 1;
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 15px;
  box-sizing: border-box;
  padding-bottom: 0;
  border-left: 1px solid var(--primary-border, #4d4d4d);
  &__lineFirst {
    width: 220px;
    height: 1px;
    background: #4d4d4d;
    margin-bottom: 16px;
  }
  &-enter,
  &-leave-to {
    right: -100%;
  }
  &-enter-active,
  &-leave-active {
    transition: right 0.5s;
  }
  &-deleteBtn {
    width: 220px;
    height: 39px;
    flex-shrink: 0;
    border-radius: 8px;
    background: #f88;
    margin-top: 18px;
    color: #fff;
    text-align: center;
    font-size: 14px;
    cursor: pointer;
  }
  &-input {
    width: 210px;
    height: 40px;
    flex-shrink: 0;
    border-radius: 4px;
    border: 1px solid #4d4d4d;
    background: #262626;
    color: #fff;
    text-align: center;
    font-size: 14px;
    font-weight: 500;
  }
}
.myIcon {
  width: 130px;
  height: 130px;
  margin-bottom: 30px;
}

.cancelConfirm-container {
  width: 252px;
  height: 133px;
  flex-shrink: 0;
  border: 1px solid #4d4d4d;
  background: rgba(38, 38, 38, 0.6);
  backdrop-filter: blur(8px);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.buttons-inner {
  display: flex;
  margin-top: 20px;
  gap: 10px;

  &__cancelBtn {
    display: flex;
    width: 88px;
    padding: 8px 28px;
    justify-content: center;
    align-items: center;
    gap: 12px;
    border-radius: 8px;
    background: #fff;
    cursor: pointer;
    outline: none;
    border: none;
    color: black;
  }
  &__confirmBtn {
    display: flex;
    width: 112px;
    padding: 8px 28px;
    justify-content: center;
    align-items: center;
    gap: 12px;
    border-radius: 8px;
    background: #fa7272;
    cursor: pointer;
    outline: none;
    border: none;
    color: white;
  }
}
</style>

<script lang="ts"></script>
