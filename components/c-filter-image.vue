<template>
  <div class="filter__image">
    <button
      class="filter__imgon"
      @click="$emit('imgOn', true)"
    >
      <svg
        :class="{ 'filter__icon-active': !imgOn }"
        class="filter__icon"
        width="18"
        height="18"
        viewBox="0 0 18 18"
        fill="#0029FF"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect
          width="18"
          height="8"
        />
        <rect
          y="10"
          width="18"
          height="8"
        />
      </svg>
    </button>
    <button
      class="filter__imgoff"
      @click="$emit('imgOn', false)"
    >
      <svg
        :class="{ 'filter__icon-active': imgOn }"
        class="filter__icon"
        width="18"
        height="18"
        viewBox="0 0 18 18"
        fill="#0029FF"
        xmlns="http://www.w3.org/2000/svg"
      >
        <rect
          width="8"
          height="8"
        />
        <rect
          y="10"
          width="8"
          height="8"
        />
        <rect
          x="10"
          width="8"
          height="8"
        />
        <rect
          x="10"
          y="10"
          width="8"
          height="8"
        />
      </svg>
    </button>
  </div>
</template>

<script>
export default {
  props: {
    imgOn: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss" scoped>
  .filter {
    &__image {
        display: flex;
    }
    &__imgon {
        padding-right: 10px;
    }
    &__icon {
        &-active {
            rect {
                fill: #C4C4C4;
            }
        }
    }
  }
</style>
