<script lang="ts" setup>
interface IDefaultButtonProps {
  disabled: boolean;
};

const {
  disabled
} = defineProps<IDefaultButtonProps>();
</script>

<template>
  <div 
    class="default-button"
    :class="{'default-button--disabled': disabled}"
  >
    <span class="default-button__text"><slot/></span>
  </div>
</template>

<style scoped>
.default-button {
  width: 100%;
  height: 100%;
  font-size: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background-color 0.5s ease;
  cursor: pointer;
  background: rgb(228, 228, 228);
  user-select: none;
}

.default-button:hover {
   background: rgb(194, 194, 194);
}

.default-button--disabled {
  pointer-events: none;
  background: rgb(247, 247, 247);
  color: grey;
}
</style>