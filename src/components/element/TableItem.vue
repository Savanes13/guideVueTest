<script lang="ts" setup>
import LineItem from './LineItem.vue';

interface ITableItemProps {
  id: number;
  name: string;
  fio: string;
  number: string;
  address: string;
};

const {
  id,
  name,
  fio,
  number,
  address,
} = defineProps<ITableItemProps>();

const emit = defineEmits<{
  (e: 'update:value', value: string, fieldName: string, id: number): void;
}>();

const updateLineValue = (value: string, fieldName: string) => {
  emit('update:value', value, fieldName, id);
};
</script>

<template>
  <div class="table-item">
    <div class="table-item__item">
      <LineItem
        :value="name"
        @update:value="(value) => updateLineValue(value, 'name')"
      />
    </div>
    <div class="table-item__item">
      <LineItem
        :value="fio"
        @update:value="(value) => updateLineValue(value, 'fio')"
      />
      <div>

      </div>
    </div>
    <div class="table-item__item">
      <LineItem
        :value="number"
        @update:value="(value) => updateLineValue(value, 'number')"
      />
    </div>
    <div class="table-item__item table-item__item--address">
      <LineItem
        :value="address"
        :is-address="true"
        @update:value="(value) => updateLineValue(value, 'address')"
      />
    </div>
    <div class="table-item__item table-item__item--empty">
      
    </div>
  </div>
</template>

<style scoped>
.table-item {
  display: flex;
  width: 100%;
}

.table-item__item {
  flex: 0 0 20%; 
  border-bottom: 1px solid rgb(119, 119, 119);
  border-top: 1px solid rgb(119, 119, 119);
  border-left: 1px solid rgb(119, 119, 119);
  height: 70px;
  padding: 20px;
  font-size: 26px
}

.table-item__item--address {
  flex-basis: 35%;
}

.table-item__item--empty {
  flex-basis: 5%;
}
</style>