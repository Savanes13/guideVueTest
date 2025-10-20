<script lang="ts" setup>

</script>

<template>
  <div class="table-header">
    <div class="table-header__item">
      <p>Название</p>
    </div>
    <div class="table-header__item">
      <div>
        <p>ФИО директора</p>
      </div>
      <div>

      </div>
    </div>
    <div class="table-header__item">
      <p>Номер телефона</p>
    </div>
    <div class="table-header__item table-header__item--address">
      <p>Адрес</p>
    </div>
    <div class="table-header__item table-header__item--empty">

    </div>
  </div>
</template>

<style scoped>
.table-header {
  display: flex;
  width: 100%;
}

.table-header__item {
  flex: 0 0 20%; 
  border-bottom: 1px solid rgb(119, 119, 119);
  border-top: 1px solid rgb(119, 119, 119);
  border-left: 1px solid rgb(119, 119, 119);
  height: 70px;
  padding: 20px;
  font-size: 26px
}

.table-header__item--address {
  flex-basis: 35%;
}

.table-header__item--empty {
  flex-basis: 5%;
}
</style>