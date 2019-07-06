<template>
  <div id="app">
    <div class="logo">
      <img alt="Vue logo" src="./assets/logo.svg">
    </div>
    <Calculator/>
  </div>
</template>

<script>
  import Calculator from './components/Calculator.vue'

  export default {
    name: 'app',
    components: {
      Calculator
    }
  }
</script>

<style lang="scss">
  @import "style/vars";

  body, html {
    margin: 0;
    padding: 0;
  }

  #app {
    height: 100%;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    background-color: map-get($color, black);

    .logo {
      width: 100%;
      background-color: map-get($color, white);

      img {
        width: 60%;
      }
    }
  }
</style>
