<template>
  <div class="header__search">
    <input
      :value="value"
      class="header__input"
      type="text"
      placeholder="Поиск по названию"
      @input="$emit('input', $event.target.value)"
    >
    <svg
      width="20"
      height="20"
      viewBox="0 0 20 20"
      fill="none"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        fill-rule="evenodd"
        clip-rule="evenodd"
        d="M8.48485 1.81818C4.80295 1.81818 1.81818 4.80295 1.81818 8.48485C1.81818 12.1667 4.80295 15.1515 8.48485 15.1515C10.2942 15.1515 11.9352 14.4307 13.1363 13.2606C13.1548 13.2382 13.1745 13.2165 13.1955 13.1956C13.2165 13.1746 13.2382 13.1549 13.2606 13.1364C14.4307 11.9352 15.1515 10.2942 15.1515 8.48485C15.1515 4.80295 12.1667 1.81818 8.48485 1.81818ZM15.093 13.8074C16.2669 12.3518 16.9697 10.5004 16.9697 8.48485C16.9697 3.7988 13.1709 0 8.48485 0C3.7988 0 0 3.7988 0 8.48485C0 13.1709 3.7988 16.9697 8.48485 16.9697C10.5004 16.9697 12.3518 16.2669 13.8074 15.0931L18.448 19.7337C18.803 20.0888 19.3786 20.0888 19.7337 19.7337C20.0887 19.3787 20.0887 18.8031 19.7337 18.4481L15.093 13.8074Z"
        fill="#DCDCDC"
      />
    </svg>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: '',
    },
    posts: {
      type: Array,
      default: [],
    },
    pages: {
      type: Array,
      default: [],
    },
    page: {
      type: Number,
      default: 1,
    },
    perPage: {
      type: Number,
      default: 4,
    },
    imgOn: {
      type: Boolean,
      default: false,
    },
    search: {
      type: String,
      default: '',
    },
    filterDomen: {
      type: String,
      default: '',
    },
  },
  watch: {
    value() {
      this.$router.push({
        name: 'id',
        params: {
          id: this.pag,
          posts: this.posts,
          imgOn: this.imgOn,
          filterDomen: this.filterDomen,
          perPage: this.perPage,
        },
        query: { search: this.search },
      });
    },
  },
};
</script>

<style lang="scss" scoped>

    .header {
        &__search {
            background-color: #ffffff;
            border-radius: 5px;
            padding: 10px;
            box-shadow: 0px 2px 10px 0px rgba(0, 0, 0, 0.05);
            display: flex;
            align-items: center;
        }
        &__input {
            color: #000;
            border: 0 solid transparent;
            outline: 0;
            background: 0 0;
            width: 250px;
        }
    }
    @media screen and (max-width: 600px) {

      .header__search {
        justify-content: space-between;
        width: 100%;
      }
    }
</style>
