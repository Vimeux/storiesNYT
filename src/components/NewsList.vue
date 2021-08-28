<template>
  <div class="newsList">
    <NewsCard v-for="(post, index) in posts" :key="index" :post="post" />
  </div>
</template>

<script>
import NewsCard from "./NewsCard.vue";

export default {
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  components: {
    NewsCard,
  },
};
</script>

<style lang="scss" scoped>
  @import "../assets/css/variable";

  .newsList{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
</style>
  
