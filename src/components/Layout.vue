<template>
  <Header/>
  <main class="layout">
    <slot/>
  </main>
  <Footer/>
</template>

<script>
import Header from "./Header.vue"
import Footer from "./Footer.vue"

export default {
  components: {
    Header,
    Footer,
  },
}
</script>

<style lang="scss" scoped>
  @import "../assets/css/variable";

  .layout{
    background-color: $color3;
  }
</style>