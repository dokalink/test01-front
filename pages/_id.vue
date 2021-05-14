<template>
  <div>
    <header class="header">
      <div class="header__wrap">
        <c-title @getUpdate="getUpdate" />
        <c-search
          v-model="search"
          :pages="pages"
          :page="page"
          :per-page="perPage"
          :posts="posts"
          :img-on="imgOn"
          :search="search"
          :filter-domen="filterDomen"
        />
      </div>
    </header>
    <div class="filter">
      <c-filter-domen
        :filter-domen="filterDomen"
        @filterDomen="filterDomen = $event"
      />
      <c-filter-image
        :img-on="imgOn"
        @imgOn="imgOn = $event"
      />
    </div>
    <c-articles
      :img-on="imgOn"
      :displayed-posts="displayedPosts"
    />
    <c-pagination
      :pages="pages"
      :page="page"
      :per-page="perPage"
      :posts="posts"
      :img-on="imgOn"
      :search="search"
      :filter-domen="filterDomen"
    />
  </div>
</template>

<script>

export default {
  layout: 'project',
  validate({ params }) {
    if (!params.id) return true;
    if (params.id === 'update') return true;
    return /^\d+$/.test(params.id);
  },
  async asyncData(context) {
    if (context.route.params.posts) { return {}; }
    const posts = await context.$axios.$get('https://inv01back.herokuapp.com/api/rss');
    return { posts };
  },
  data() {
    return {
      posts: this.$route.params.posts ? this.$route.params.posts : [''],
      page: this.$route.params.id ? Number.parseInt(this.$route.params.id, 10) : 1,
      perPage: this.$route.params.perPage ? Number.parseInt(this.$route.params.perPage, 10) : 4,
      pages: [],
      // search: this.$route.params.search ? this.$route.params.search : '',
      search: this.$route.query.search ? this.$route.query.search : '',
      filterDomen: this.$route.params.filterDomen ? this.$route.params.filterDomen : '',
      imgOn: this.$route.params.imgOn ? this.$route.params.imgOn : false,
    };
  },
  computed: {
    displayedPosts() {
      return this.paginate(this.displayFilter);
    },

    displayFilter() {
      return this.posts.filter((a) => {
        if (a) {
          const searchString = `${a.title} ${a.content}`;
          return (searchString.toLowerCase().indexOf(this.search.toLowerCase()) !== -1)
                    && (a.linkdom.indexOf(this.filterDomen) !== -1);
        }
        return false;
      });
    },
  },
  watch: {

    imgOn() {
      this.imgOn ? this.perPage = 3 : this.perPage = 4;
      this.setPages();
    },
    displayFilter() {
      this.setPages();
    },
    filterDomen() {
      this.setPages();
    },
  },

  created() {
    this.setPages();
  },
  methods: {
    getUpdate() {
      this.$route.path === '/' ? this.$router.push('/1') : this.$router.push('/');
    },

    setPages() {
      const numberOfPages = Math.ceil(this.displayFilter.length / this.perPage);
      this.pages = [];
      for (let index = 1; index <= numberOfPages; index++) {
        this.pages.push(index);
      }
    },
    paginate(posts) {
      const { page } = this;
      const { perPage } = this;
      const from = (page * perPage) - perPage;
      const to = (page * perPage);
      return posts.slice(from, to);
    },

  },
};
</script>

<style lang="scss" scoped>
  @media screen and (max-width: 600px) {
    .header__wrap {
      flex-direction: column;
    }
  }

  .header {
  &__wrap {
     display: flex;
     justify-content: space-between;
     border-bottom: #E5E5E5 solid 1px;
     padding: 36px 0 36px 0;
     align-items: center;
   }
  }
  .filter {
    display: flex;
    justify-content: space-between;
    padding: 26px 0 28px 0;
    font-size: 14px;
    font-weight: bold;
  }

</style>
