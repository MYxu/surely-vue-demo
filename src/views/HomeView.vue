<template>
  <div class="container">
    <div class="title">home page</div>
    <a-input v-model="inputVal" style="width: 200px; margin: 20px"/>
    <s-table
      ref="sTableRef"
      :columns="columns"
      :scroll="{ y: 400, x: 1200 }"
      :pagination="false"
      :data-source="data"
    />
  </div>
</template>
<script lang="ts">
export default {
  name: 'Home'
}
</script>
<script setup lang="ts">
import STable from "@surely-vue/table";
import type {STableColumnsType} from '@surely-vue/table';
import { onActivated, onDeactivated, reactive, ref, onMounted } from 'vue';
import { useScroll } from '@vueuse/core'

interface DataItem {
  key: number;
  name: string;
  age: number;
  gender: string;
  phone: string;
  address: string;
}

const inputVal = ref(12)

const columns: STableColumnsType = [
  {
    title: 'Full Name',
    dataIndex: 'name',
    width: 100,
  },
  {
    title: 'Age',
    dataIndex: 'age',
    width: 100,
  },
  {
    title: 'Gender',
    dataIndex: 'gender',
    width: 100,
  },
  {
    title: 'Phone',
    dataIndex: 'phone',
    width: 200,
  },
  {title: 'Address1', dataIndex: 'address', autoHeight: true, resizable: true},
  {title: 'Address2', dataIndex: 'address', autoHeight: true, resizable: true},
];
const data: DataItem[] = reactive([]);
for (let i = 0; i < 1000; i++) {
  data.push({
    key: i,
    name: `Edrward ${i}`,
    age: i + 1,
    gender: 'Female',
    phone: '123456798665xxx',
    address: `xxx xxx xxx London Park no. ${i}`,
  });
}
const sTableRef = ref();
let scrollTop = 0;
function onStopScroll(e) {
  scrollTop = e.srcElement.scrollTop
}
onMounted(() => {
  useScroll(sTableRef.value.body, { onStop: onStopScroll })
})


onDeactivated(() => {
  console.log('home page last scrollTop: ' + scrollTop)
});

onActivated(() => {
  if (scrollTop) {
    sTableRef.value.scrollTo(scrollTop);
  }
})
</script>
<style lang="less">
.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;

  .title {
    font-weight: bolder;
    font-size: 30px;
  }
}
</style>

