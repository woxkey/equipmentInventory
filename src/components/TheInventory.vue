<script setup lang="ts">
import { ref, watch, type Ref } from "vue";
import GreenFolderIcon from "./icons/IconGreenFolder.vue";
import YellowFolderIcon from "./icons/IconYellowFolder.vue";
import BlueFolderIcon from "./icons/IconBlueFolder.vue";
import TheModalVue from "./TheModal.vue";
import SideBar from "./SideBar.vue";
import TheFooterVue from "./TheFooter.vue";

export interface Item {
  id: number;
  items: number;
}

const items: Ref<Item[]> = ref([]);
const show: Ref<boolean> = ref(false);
const selectedItem: Ref<number> = ref(0);
const selectedType: Ref<string> = ref("");

const storedItems = localStorage.getItem("items");

if (storedItems) {
  items.value = JSON.parse(storedItems);
} else {
  items.value = [
    { id: 0, items: 3 },
    { id: 1, items: 5 },
    { id: 2, items: 4 },
  ];
}

watch(
  items,
  (newItems) => {
    localStorage.setItem("items", JSON.stringify(newItems));
  },
  { deep: true }
);

const startDrag = (event: DragEvent | any, index: number) => {
  event.dataTransfer.dropEffect = "move";
  event.dataTransfer.effectAllowed = "move";
  event.dataTransfer.setData("itemId", index);
};

const onDrop = (event: DragEvent | any, index: number) => {
  const itemId = event.dataTransfer.getData("itemId");
  const item = items.value.find((item) => item.id === parseInt(itemId));
  const itemExists = items.value.some((item) => item.id === index);
  if (!itemExists) {
    item!.id = index;
  }
};

const handleClick = (id: number, type: string) => {
  show.value = !show.value;
  selectedItem.value = id;
  selectedType.value = type;
};

const updateValue = (newValue: boolean) => {
  show.value = newValue;
};
</script>

<template>
  <div class="myContainer">
    <div class="myContainer-inner">
      <SideBar />
      <div class="inventory">
        <TheModalVue
          :my-show="show"
          :update-value="updateValue"
          :selectedItemId="selectedItem"
          :items="items"
          :selectedType="selectedType"
        />
        <div
          class="inventory-item"
          @drop="onDrop($event, index - 1)"
          @dragenter.prevent
          @dragover.prevent
          :key="index"
          v-for="index in 25"
        >
          <div
            class="inventory-item-folder"
            @click="handleClick(items[0].id, 'green')"
            @dragstart="startDrag($event, items[0].id)"
            v-if="index - 1 === items[0].id"
            draggable="true"
          >
            <GreenFolderIcon />
            <div class="inventory-item-folder-count">
              {{ items[0].items }}
            </div>
          </div>
          <div
            class="inventory-item-folder"
            @click="handleClick(items[1].id, 'yellow')"
            @dragstart="startDrag($event, items[1].id)"
            v-if="index - 1 === items[1].id"
            draggable="true"
          >
            <YellowFolderIcon />
            <div class="inventory-item-folder-count">
              {{ items[1].items }}
            </div>
          </div>
          <div
            class="inventory-item-folder"
            @click="handleClick(items[2].id, 'blue')"
            @dragstart="startDrag($event, items[2].id)"
            v-if="index - 1 === items[2].id"
            draggable="true"
          >
            <BlueFolderIcon />
            <div class="inventory-item-folder-count">
              {{ items[2].items }}
            </div>
          </div>
        </div>
      </div>
    </div>
    <TheFooterVue />
  </div>
</template>

<style scoped lang="scss">
.myContainer {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  &-inner {
    display: flex;
    justify-content: center;
    padding-bottom: 24px;
  }
}

.inventory {
  display: grid;
  position: relative;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr;
  width: 500px;
  height: 500px;
  border-radius: 12px;
  background-color: #262626;
  border-collapse: separate;
  overflow: hidden;
  box-sizing: border-box;
  &-item {
    border: 1px solid #4d4d4d;
    display: flex;
    justify-content: center;
    align-items: center;
    &-folder {
      position: relative;
      cursor: pointer;
      &-count {
        position: absolute;
        display: inline;
        border: 1px solid #4d4d4d;
        border-radius: 6px 0px 0px 0px;
        width: 16px;
        height: 16px;
        left: 60px;
        font-size: 10px;
        display: flex;
        justify-content: center;
        align-items: center;
        top: 62px;
        color: #fff;
        text-align: center;
        font-size: 10px;
        font-weight: 500;
        opacity: 0.4000000059604645;
      }
    }
  }
}
</style>
