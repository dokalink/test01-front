<template>
  <div class="filter__domen">
    <button
      :class="{ 'filter__domitem-active': filterDomen === '' }"
      class="filter__domitem"
      @click="$emit('filterDomen','')"
    >
      Все
    </button>
    <button
      :class="{ 'filter__domitem-active': filterDomen === 'www.lenta.ru' }"
      class="filter__domitem"
      @click="$emit('filterDomen','www.lenta.ru')"
    >
      Lenta.ru
    </button>
    <button
      :class="{ 'filter__domitem-active': filterDomen === 'www.mos.ru' }"
      class="filter__domitem"
      @click="$emit('filterDomen','www.mos.ru')"
    >
      Mos.ru
    </button>
  </div>
</template>

<script>
export default {
  props: {
    filterDomen: {
      type: String,
      default: '',
    },
  },
};
</script>

<style lang="scss" scoped>
    .filter {
      &__domen {
        cursor: pointer;
        display: flex;
      }
      &__domitem {
          &-active {
           color: #000000;
           }
           padding-right: 6px;
           color: #0029FF;
        }
    }
</style>
