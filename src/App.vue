<script setup lang="ts">
import { computed, ref } from 'vue';
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
  },
  {
    id: 3,
    name: 'ИП erwer."',
    fio: 'Сидоров С.С.',
    number: '+7 000 56 78 99',
    address: {
      city: "г. Санкт-Петербург",
      street: "пр.Невский",
      house: "д. 2"
    }
  },
  {
    id: 4,
    name: 'ИП ggg"',
    fio: 'Сидоров С.С.',
    number: '+7 000 56 78 99',
    address: {
      city: "г. Санкт-Петербург",
      street: "пр.Невский",
      house: "д. 2"
    }
  },
  {
    id: 5,
    name: 'ИП ggg"',
    fio: 'Сидоров С.С.',
    number: '+7 000 56 78 99',
    address: {
      city: "г. Санкт-Петербург",
      street: "пр.Невский",
      house: "д. 2"
    }
  },
  {
    id: 6,
    name: 'ИП ggg"',
    fio: 'Сидоров С.С.',
    number: '+7 000 56 78 99',
    address: {
      city: "г. Санкт-Петербург",
      street: "пр.Невский",
      house: "д. 2"
    }
  },
  {
    id: 7,
    name: 'ИП ggg"',
    fio: 'Сидоров С.С.',
    number: '+7 000 56 78 99',
    address: {
      city: "г. Санкт-Петербург",
      street: "пр.Невский",
      house: "д. 2"
    }
  }
]);

const elementsOnPage = ref<number>(3);
const startPage = ref<number>(1);

const nowPage = computed(() => {
  const arrLength = tableDataArr.value.length;
  const maxPage = Math.ceil(arrLength / elementsOnPage.value);
  if((elementsOnPage.value * startPage.value) > arrLength + elementsOnPage.value) return maxPage;
  if(startPage.value < 1) return 1;
  return startPage.value;
});

//сделать массив выбранной страницы
const arrByPage = computed(() => {
  const lastItem = elementsOnPage.value * nowPage.value;
  const firstItem = elementsOnPage.value * nowPage.value - elementsOnPage.value;
  const arr = tableDataArr.value.slice(firstItem, lastItem)
  return arr
});

const nextPage = () => {
  const arrLength = tableDataArr.value.length;
  if((elementsOnPage.value * startPage.value + 1) >= arrLength + elementsOnPage.value) return;
  startPage.value ++;
};

const backPage = () => {
  if(startPage.value <= 1) return;
  startPage.value --;
};
</script>

<template>
  <div>
    {{ nowPage }}

    {{ arrByPage }}

    {{ startPage }}

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

    <div>
      <button @click="backPage">назад</button>
      <button @click="nextPage">вперед</button>
    </div>
  </div>
</template>

<style scoped>

</style>
