<script lang="ts" setup>
import { computed} from 'vue';

interface IEmailInputProps {
  value: string;
  placeholder: string;
};

let {
  value,
  placeholder
} = defineProps<IEmailInputProps>();

const emit = defineEmits<{
  (e: 'update:value', value: string): void;
}>();

const inputValue = computed({
  get: () => value,
  set: (newValue: string) => {
    emit('update:value', newValue)
  }
});
</script>

<template>
  <input
    class="input"
    :placeholder="placeholder"
    v-model="inputValue"
  >
</template>

<style scoped>
.input {
  width: 100%;
  height: 100%;
  font-size: 22px;
  padding: 10px;
}
</style>