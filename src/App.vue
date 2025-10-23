<script setup lang="ts">
import { computed, ref, watch } from 'vue';
import HeaderTable from './components/element/HeaderTable.vue';
import DefaultButton from './components/ui/button/DefaultButton.vue';
import TableItem from './components/element/TableItem.vue';
import DefaultIInput from './components/ui/input/DefaultIInput.vue';

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

const searchInputValue = ref<string>('');
const elementsOnPage = ref<number>(3);
const currentPage = ref<number>(1);

const filterArr = computed(() => {
  if (!searchInputValue.value) return tableDataArr.value;
  const query = searchInputValue.value.toLowerCase().trim();
  return tableDataArr.value.filter(item =>
    item.fio.toLowerCase().includes(query)
  );
});

const totalPages = computed(() => {
  return Math.max(1, Math.ceil(filterArr.value.length / Math.max(1, elementsOnPage.value)));
});

const isFirstPage = computed(() => currentPage.value <= 1);
const isLastPage = computed(() => currentPage.value >= totalPages.value);

const arrByPage = computed(() => {
  const perPage = Math.max(1, elementsOnPage.value);
  const page = Math.max(1, currentPage.value);
  const first = (page - 1) * perPage;
  const last = page * perPage;
  return filterArr.value.slice(first, last);
});

watch([filterArr, elementsOnPage], () => {
  if (currentPage.value > totalPages.value) currentPage.value = totalPages.value;
  if (currentPage.value < 1) currentPage.value = 1;
}, { immediate: true });

const nextPage = () => {
  if (currentPage.value < totalPages.value) currentPage.value++;
};

const backPage = () => {
  if (currentPage.value > 1) currentPage.value--;
};

const changeField = (value: string, fieldName: string, id: number) => {
  const tableItem = tableDataArr.value.find(item => item.id === id);
  if (tableItem) (tableItem as any)[fieldName] = value;
};

const deteleArrItem = (id: number) => {
  tableDataArr.value = tableDataArr.value.filter(item => item.id !== id);
};
</script>

<template>
  <div class="app">
    <div class="app__search">
      <DefaultIInput
        v-model:value="searchInputValue"
        placeholder="Найти по ФИО..."
      />
    </div>

    <div class="app__table">
      <HeaderTable/>
      <TableItem
        v-for="item in arrByPage"
        :key="item.id"
        :id="item.id"
        :name="item.name"
        :fio="item.fio"
        :number="item.number"
        :address="item.address"
        @update:value="changeField"
        @delete="deteleArrItem"
      />
    </div>

    <div class="app__managed-table">
      <div class="button-block">
        <DefaultButton
          class="button-block__button"
          @click="backPage"
          :disabled="isFirstPage"
        >
          назад
        </DefaultButton>
        <DefaultButton
          class="button-block__button"
          @click="nextPage"
          :disabled="isLastPage"
        >
          вперед
        </DefaultButton>
      </div>
      <div class="info-block">
        <div class="info-block">
          <p>Блоков на странице: {{ elementsOnPage }}</p>
        </div>
        <div class="info-block">
          <p>Страница: {{ currentPage }}</p>
        </div>
      </div>
    </div>

  </div>
</template>

<style scoped>
.app {
  
}

.app__search {
  width: 700px;
  margin: 20px;
}

.app__table {
  height: 280px;
}

.app__managed-table {
  margin-top: 20px;
  margin-left: 20px;
  display: flex;
  align-items: center;
  gap: 20px;
}

.info-block {
  display: flex;
  gap: 10px;
  font-size: 20px;
}

.button-block {
  display: flex;
  gap: 10px;
}

.button-block__button {
  width: 200px;
  height: 50px;
  border-radius: 4px;
}
</style>
