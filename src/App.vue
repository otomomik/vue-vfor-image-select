<template>
  <div>
    <template v-for="image in IMAGE_LIST" :key="image.id">
      <img
        :src="image.path"
        :class="{
          selected: checkSelectImage(image.id),
        }"
        @click="handleClickImage(image)"
        :alt="image.name"
      />
    </template>
  </div>
  <div>
    {{ selectImages.map(({ name }) => name).join(" ") }}
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";
import VueSVG from "./assets/vue-svgrepo-com.svg";
import ReactSVG from "./assets/react-svgrepo-com.svg";
import AngularSVG from "./assets/angular-svgrepo-com.svg";

type Image = {
  id: string;
  name: string;
  path: any;
};

const IMAGE_LIST: Image[] = [
  {
    id: "vue",
    name: "Vue",
    path: VueSVG,
  },
  {
    id: "react",
    name: "React",
    path: ReactSVG,
  },
  {
    id: "angular",
    name: "Angular",
    path: AngularSVG,
  },
];

const selectImages = ref<Image[]>([]);

const checkSelectImage = (id: Image["id"]) => {
  return selectImages.value.some((image) => image.id === id);
};

const handleClickImage = (image: Image) => {
  const foundImageIndex = selectImages.value.findIndex(
    ({ id }) => id === image.id
  );
  if (foundImageIndex === -1) {
    // 未選択
    selectImages.value.push(image);
  } else {
    // 選択済み
    selectImages.value.splice(foundImageIndex, 1);
  }
};
</script>

<style scoped>
img {
  width: 80px;
}
img.selected {
  outline: 1px solid red;
}
</style>
