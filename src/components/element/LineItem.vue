<script lang="ts" setup>
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
</script>

<template>
  <div class="line-item">
    <div v-if="!isAddress">
      <p>{{ value }}</p>
    </div>
    <div v-else>
      <p v-if="isAddressValue(value)">{{ value.city }}, {{ value.street }}, {{ value.house }}</p>
    </div>
  </div>
</template>

<style scoped>

</style>