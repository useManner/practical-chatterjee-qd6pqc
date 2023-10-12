<template>
  <div>
    <el-check-tag
      v-for="key in list"
      :checked="key === checked"
      @click="onChange(key)"
      :key="key"
      >{{ key === "all" ? "全部" : key }}</el-check-tag
    >
    <div v-for="item in filteredList" :key="item.key">
      {{ item.value }}
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const list = ref([11, 22, 33, 44, 55]);
const list_child = ref([
  { key: 11, value: "11是我" },
  { key: 22, value: "22是我" },
  { key: 33, value: "33是我" },
  { key: 44, value: "44是我" },
  { key: 55, value: "55是我" },
]);

list.value.unshift("all");

const checked = ref(list.value[0]);

const onChange = (status) => {
  checked.value = status;
};

const filteredList = computed(() => {
  if (checked.value === "all") {
    return list_child.value;
  } else {
    return list_child.value.filter((item) => item.key === checked.value);
  }
});
</script>
