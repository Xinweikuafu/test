<template>
  <uni-data-select :disabled="disabled" clear v-bind="$attrs" :placeholder="'请选择'+title" :localdata="selectData"
                   :filter="true">

  </uni-data-select>
</template>

<script setup>
import {onLoad} from "@dcloudio/uni-app";

const {proxy} = getCurrentInstance();
const props = defineProps({
  api: {type: String, default: ''},
  disabled: {type: Boolean, default: false},
  title: {type: String, default: ""}
});
const selectData = ref([]);

onLoad(() => {
  refresh();
});

function refresh() {
  getApiData();
}

async function getApiData() {
  let response = await apiMethod();
  selectData.value = response.data;
}

function apiMethod() {
  return props.api.split('.').reduce((acc, item) => acc[item], proxy.$api)();
}

</script>