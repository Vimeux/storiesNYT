<template>
  <header class="header">
    <img alt="Vue logo" src="../assets/images/logo.png"  class="header-logo"/>
    <span class="header-title">
      Vue News | NYTimes Edition
    </span>
  </header>
</template>

<style lang="scss" scoped>
@import '../assets/css/variable';
  .header{
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: $color1;
    &-logo{
      width: 50px;
      margin: 10px;
    }
    &-title{
      font-family: $text;
      font-weight: 600;
      font-size: 25px;
      color: $colorWhite;
    }
  }
</style>