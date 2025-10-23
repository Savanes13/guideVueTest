<script lang="ts" setup>
import { ref, watch } from 'vue'

interface IAddress {
  city: string
  street: string
  house: string
}

interface ILineItemProps {
  value: string | IAddress
  isAddress?: boolean
}

const {
  value,
  isAddress = false
} = defineProps<ILineItemProps>();

const isAddressValue = (value: string | IAddress): value is IAddress => {
  return typeof value !== 'string'
}

const inputValue = ref<string>(isAddressValue(value) ? `${value.city}, ${value.street}, ${value.house}` : value);

const emit = defineEmits<{
  (e: 'update:value', value: string): void;
}>();

watch(inputValue, () => {
  updateValue();
})

const updateValue = () => {
  emit('update:value', inputValue.value);
};
</script>

<template>
  <div class="line-item">
    <div>
      <div v-if="!isAddress">
        <p>{{ value }}</p>
      </div>
      <div v-else>
        <p v-if="isAddressValue(value)">{{ value.city }}, {{ value.street }}, {{ value.house }}</p>
      </div>
    </div>

    <div>
      <input 
        type="text"
        v-model="inputValue"
      >
    </div>

  </div>
</template>

<style scoped>

</style>