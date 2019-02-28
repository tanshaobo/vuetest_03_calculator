<template>
  <div id="app">
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/calculator'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style lang="stylus">
body
  background linear-gradient(90deg,#85D8CE, #085078)
#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
</style>
