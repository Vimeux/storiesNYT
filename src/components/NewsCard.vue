<template>
  <section class="news">
    <a class="news-container" :href="post.url" target="_blank" rel="noreferrer">
      <div>
        <h3 class="news-title">{{ post.title }}</h3>
        <img class="news-image" :src="post.thumbnail" :alt="post.caption" />
        <p class="news-abstract">
          {{ post.abstract }}
        </p>
      </div>
      <div>
        <p class="news-autor">{{ post.byline }}</p>
        <p class="news-date">{{ formatDate(post.published_date) }}</p>
      </div>
    </a>
  </section>
</template>

<script>
import { format } from "date-fns";

export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
  methods: {
    formatDate(strDate) {
      return format(new Date(strDate), "MMMM do, yyyy");
    },
  },
};
</script>

<style lang="scss" scoped>
@import "../assets/css/variable";

.news {
  width: 300px;
  height: auto;
  background-color: $colorWhite;
  padding: 20px;
  margin: 20px;
  border-radius: 15px;
  transition: all 0.5s;
  &-container{
    height: 100%;
    text-decoration: none;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
  &-title{
    color: $color1;
    line-height: 1.5;
    font-size: 20px;
    margin: 0 0 20px 0;
  }
  &-image{
    width: 100%;
    height: auto;
    border-radius: 5px;
  }
  &-abstract{
    color: $color1;
    line-height: 1.3;
  }
  &-autor{
    color: $color2;
    font-weight: 600;
    text-align: end;
    line-height: 1.5;
  }
  &-date{
    color: $color2;
    font-weight: 400;
    text-align: end;
  }
  &:hover{
    transform: scale(1.06);
  }
}
</style>
