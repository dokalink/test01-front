<template>
  <div class="article__wrapper">
    <div class="article__header">
      <div
        v-show="imgOn"
        class="article__imagebox"
      >
        <img
          class="article__image"
          :src="post.img"
          :alt="post.title"
        >
      </div>
      <div>
        <h2 class="article__title">
          <a
            class="article__titlelink"
            :href="post.link"
            target="_blank"
          >{{ post.title }}</a>
        </h2>
        <div class="article__content">
          {{ post.content }}
        </div>
      </div>
    </div>

    <div class="article__footer">
      <a
        v-show="!imgOn"
        class="article__link"
        :href="post.link"
        target="_blank"
      >Подробнее</a>
      <div class="article__footer article__footer-align">
        <div class="article__url">
          {{ post.linkdom }}
        </div>
        <div class="article__date">
          {{ post.date }}
        </div>
      </div>
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
    post: {
      type: Object,
      default: {},
    },
  },
};
</script>

<style lang="scss" scoped>


  .article {
    &__header{
      display: flex;
    }
    &__title {
      color: #0029FF;
      font-size: 18px;
      font-weight: 700;
      padding-bottom: 25px;
    }
    &__titlelink {
      text-decoration: none;
    }
    &__content {
      font-size: 14px;
      margin-bottom: 27px;
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-box;
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
    }
    &__link {
      font-size: 14px;
      font-weight: 400;
      color: #0029FF;
    }
    &__imagebox {
      margin-right: 30px;
    }
    &__image {
      width: 200px;
      height: 100px;
      object-fit: cover;
    }
    &__wrapper {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      height: 100%;
    }
  }
  .article__footer {
    padding-top: 14px;
    color: #DCDCDC;
    font-size: 14px;
    &-align {
      display: flex;
      justify-content: space-between;
    }
  }
  @media screen and (max-width: 600px) {

    .article__header {
      flex-direction: column;
    }
    .article__content {
      -webkit-line-clamp: 3;
    }
    .article__imagebox {
      margin-right: 0px;
    }
    .article__image {
      width: 100%;
      height: auto;
    }
  }
</style>
