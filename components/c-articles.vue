<template>
  <div class="articles">
    <div
      v-for=" post in displayedPosts"
      :key="post.link"
      class="articles__article article"
      :class="{ 'articles__article-imgon': imgOn }"
    >
      <c-article
        :post="post"
        :img-on="imgOn"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imgOn: {
      type: Boolean,
      default: false,
    },
    displayedPosts: {
      type: Array,
      default: [],
    },
  },
};

</script>

<style lang="scss" scoped>

  .article {
    padding: 30px 30px 4px;
    background-color: #ffffff;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    box-shadow: 0px 2px 10px 0px rgba(0, 0, 0, 0.05);
  }

  .articles {
    display: flex;
    flex-wrap:wrap;
    justify-content: flex-start;
    margin: 0 -10px;
    &__article {
      width: calc(1/2*100% - 20px);
      margin: 10px;
      }
    &__article-imgon {
      width: calc(100% - 20px);
    }
  }

  @media screen and (max-width: 600px) {
    .article {
      width: calc(1 / 1 * 100% - 20px);
    }
  }
</style>
