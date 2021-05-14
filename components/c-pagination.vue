<template>
  <nav class="pagination">
    <div
      v-for="pag in paginations"
    >
      <p v-if="pag === '...'">
        ...
      </p>
      <nuxt-link
        v-if="pag !== '...'"
        :to="linkPage(pag)"

        class="pagination__item"
        :class="{ 'link-active': linkActive & pag == 1}"
      >
        {{ pag }}
      </nuxt-link>
    </div>
  </nav>
</template>

<script>
export default {
  props: {
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
  computed: {
    linkActive() {
      if (!this.$route.params.id) { return true; }
      return false;
    },
    paginations() {
      const pagMas = [];
      if (this.page > 3) { pagMas.push('1', '...'); }
      const mas = this.pages.slice(this.pageStart(this.page, this.pages.length),
        this.pageEnd(this.page, this.pages.length));
      mas.forEach(
        (item, i, arr) => {
          pagMas.push(arr[i]);
        },
      );

      if (this.page < (this.pages.length - 3)) { pagMas.push('...', this.pages.length); }

      return pagMas;
    },
  },

  methods: {
    linkPage(pag) {
      const linkTmp = {
        name: 'id',
        params:
                {
                  id: pag,
                  posts: this.posts,
                  imgOn: this.imgOn,
                  filterDomen: this.filterDomen,
                  perPage: this.perPage,
                },
      };
      if (!(this.search === '')) linkTmp.query = { search: this.search };
      return linkTmp;
    },

    pageStart(carentPage, maxPages) {
      if (carentPage < 4) {
        return 0;
      }
      if (carentPage > (maxPages - 3)) {
        return maxPages - 5;
      }
      return carentPage - 3;
    },
    pageEnd(carentPage, maxPages) {
      if (carentPage < 3) {
        return 5;
      }
      if (carentPage > (maxPages - 2)) {
        return maxPages;
      }
      return carentPage + 2;
    },
  },
};
</script>

<style lang="scss" >
  .pagination {
     .nuxt-link-active, .link-active{
       color: #0029ff;
     }
    display: flex;
    justify-content: center;
    font-size: 18px;
    font-weight: bold;
    cursor: pointer;
    padding: 50px 0 20px;
    &__item {
      padding: 10px;
      color: #000000;
      text-decoration: none;
    }

  }
</style>
