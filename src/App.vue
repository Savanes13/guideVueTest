<script setup lang="ts">
import { computed, ref, watch } from 'vue';
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
const currentPage = ref<number>(1);

const totalPages = computed(() => {
  return Math.max(1, Math.ceil(tableDataArr.value.length / Math.max(1, elementsOnPage.value)));
});

const isFirstPage = computed(() => currentPage.value <= 1);
const isLastPage = computed(() => currentPage.value >= totalPages.value);

const arrByPage = computed(() => {
  const perPage = Math.max(1, elementsOnPage.value);
  const page = Math.max(1, currentPage.value);
  const first = (page - 1) * perPage;
  const last = page * perPage;
  return tableDataArr.value.slice(first, last);
});

watch([tableDataArr, elementsOnPage], () => {
  if (currentPage.value > totalPages.value) currentPage.value = totalPages.value;
  if (currentPage.value < 1) currentPage.value = 1;
}, { immediate: true });

const nextPage = () => {
  if (currentPage.value < totalPages.value) currentPage.value++;
};

const backPage = () => {
  if (currentPage.value > 1) currentPage.value--;
};
</script>

<template>
  <div>
    <HeaderTable/>
    <TableItem
      v-for="item in arrByPage"
      :key="item.id"
      :id="item.id"
      :name="item.name"
      :fio="item.fio"
      :number="item.number"
      :address="item.address"
    />

    <div>
      <div>
        <p>блоков на странице {{ elementsOnPage }}</p>
      </div>
      <div>
        <p>Страница {{ currentPage }}</p>
      </div>
    </div>

    <div>
      <button @click="backPage">назад</button>
      <button @click="nextPage">вперед</button>
    </div>
  </div>
</template>

<style scoped>

</style>
