<script setup lang="ts">
import { ref } from 'vue';
import HeaderTable from './components/element/HeaderTable.vue';

import TableItem from './components/element/TableItem.vue';


const tableDataArr = ref([
  {
    id: 1,
    name: 'ООО"Вектор"',
    fio: 'Иванов И.И.',
    number: '+7 000 123 45 67',
    address: {
      city: "г. Москва",
      street: "ул. Ленина",
      house: "д. 1"
    }
  },
  {
    id: 2,
    name: 'ИП СидоровС.С."',
    fio: 'Сидоров С.С.',
    number: '+7 000 56 78 99',
    address: {
      city: "г. Санкт-Петербург",
      street: "пр.Невский",
      house: "д. 2"
    }
  }
])
</script>

<template>
  <div>
    <HeaderTable/>

    <TableItem
      v-for="item in tableDataArr"
      :key="item.id"
      :id="item.id"
      :name="item.name"
      :fio="item.fio"
      :number="item.number"
      :address="item.address"
    />
  </div>
</template>

<style scoped>

</style>
