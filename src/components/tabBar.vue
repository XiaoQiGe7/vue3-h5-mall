<script lang="ts">
export default {
  name: "TabBar",
};
</script>

<script setup lang="ts">
import { ref } from "vue";
interface tabProps {
  data?: [
    {
      id: string;
      to: string;
      name: string;
      icon: string;
      iconActive: string;
    }
  ];
}
const props = defineProps<tabProps>();
const emit = defineEmits(["change"]);
const active = ref("home");
const onChange = (value) => {
  emit("change", value);
};
const getIconUrl = (name: string) => {
  const path = `../assets/icon${name}.png`;
  const iconModules = import.meta.globEager("../assets/icon/*.png");
  const aaa = iconModules[path].default;
  return aaa;
};
</script>

<template>
  <van-tabbar
    fixed
    route
    v-model="active"
    @change="onChange"
    active-color="#000000"
    inactive-color="#959595"
  >
    <van-tabbar-item
      v-for="item in props.data"
      :key="item.id"
      :to="item.to"
      :name="item.name"
    >
      <span>{{ item.name }}</span>
      <template #icon="props">
        <van-icon
          :name="item.icon"
          :color="props.active ? '#000000' : '#959595'"
        />
      </template>
    </van-tabbar-item>
  </van-tabbar>
</template>

<style scoped>
.icon {
  width: 20px;
  height: 20px;
}
</style>