<template>
  <footer class="footer">
    <p class="footer-copyright">Copyright© 2021 BenjaminVimeux</p>
    <p class="footer-copyright">Projet réaliser à partir du tutoriel <a href="https://www.sitepoint.com/fetching-data-third-party-api-vue-axios/" target="_blank">Récupérer des données à partir d'une API tierce avec Vue.js et Axios</a> par le site SitePoint</p>
  </footer>
</template>

<style lang="scss" scoped>
@import "../assets/css/variable";
.footer {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: $color1;
  &-copyright {
    font-family: $text;
    font-weight: 600;
    font-size: 15px;
    color: $colorWhite;
    margin: 20px;
    text-align: center;
    a{
      color: $color4;
      &:hover{
        color: $color5;
      }
    }
  }
}
</style>
