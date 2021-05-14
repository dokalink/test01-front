<template>
  <div class="header__title">
    <h1>Список новостей</h1>
    <c-update @getUpdate="$emit('getUpdate')" />
  </div>
</template>

<script>

</script>

<style lang="scss" scoped>

  .header {
  &__title {
     display: flex;
     align-items: center;
   }
  }

  @media screen and (max-width: 600px) {

    .header__title {
      justify-content: space-between;
      width: 100%;
      margin-bottom: 10px;
    }
  }
</style>
