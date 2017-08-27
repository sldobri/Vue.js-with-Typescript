<template lang="pug">
  #app
    img(src='./assets/logo.png')
    router-view
</template>

<script lang="ts">
  export default {
    name: 'app'
  }
</script>

<style lang="stylus">
#app
  margin-top 60px
  color #2c3e50
  text-align center
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
</style>
