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

const { value, isAddress = false } = defineProps<ILineItemProps>();

const isAddressValue = (val: string | IAddress): val is IAddress => {
  return typeof val !== 'string'
}

const isEditing = ref<boolean>(false);
const inputValue = ref<string>(
  isAddressValue(value) ? `${value.city}, ${value.street}, ${value.house}` : (value as string)
);

const emit = defineEmits<{
  (e: 'update:value', value: string): void;
}>()

watch(inputValue, () => {
  updateValue();
});

const updateValue = () => {
  emit('update:value', inputValue.value)
}

const startEditing = () => {
  isEditing.value = true;
};

const stopEditing = () => {
  isEditing.value = false;
};
</script>

<template>
  <div class="line-item">
    <div>
      <div 
        v-if="!isEditing" 
        @click="startEditing" 
        style="cursor: text;"
      >
        <p v-if="!isAddress">{{ value }}</p>
        <p v-else-if="isAddressValue(value)">{{ value.city }}, {{ value.street }}, {{ value.house }}</p>
      </div>
      <div v-else>
        <input 
          type="text" 
          v-model="inputValue" 
          @blur="stopEditing"
          autofocus
        />
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
