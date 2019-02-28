<template>
  <div class="calculator">
    <button v-on:click="changeModeEvent" class="toggle-btn">
      <p v-if="changeMode">轻奢版</p>
      <p v-else>豪华版</p>
    </button>
    <div class="results">
      <input class="input" v-model="current">
    </div>
    <!--轻奢版-->
    <div class="mode" v-if="changeMode">
      <button v-bind:class="{'btn':true,'lang-btn':(item === '=')}" v-for="item in baseBtns" v-on:click="press" v-bind:key='item.index'>{{item}}</button>
    </div>
    <!--豪华版-->
    <div class="mode" v-else>
      <button v-bind:class="{'btn':true,'lang-btn':(item === '=')}" v-for="item in richBtns" v-on:click="press" v-bind:key='item.index'>{{item}}</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',
  data () {
    return {
      current: '',
      changeMode: true,
      baseBtns: ['7', '8', '9', '*', '<=', 'C', '4', '5', '6', '/', '(', ')', '1', '2', '3', '-', 'x ²', '±', '0', '.', '%', '+', '='],
      richBtns: ['sin', 'cos', 'tan', 'x^', '<=', 'C', 'log', 'ln', 'e', 'o', 'rad', '√', '7', '8', '9', '/', 'x ²', 'x !', '4', '5', '6', '*', '(', ')', '1', '2', '3', '-', '%', '±', '0', '.', 'π', '+', '=']
    }
  },
  methods: {
    changeModeEvent () {
      let that = this
      that.changeMode = !that.changeMode
    },
    press (event) {
      let that = this
      let key = event.target.textContent
      console.log(that.current)
      if (
        key !== '=' &&
        key !== 'C' &&
        key !== '*' &&
        key !== '/' &&
        key !== '√' &&
        key !== 'x ²' &&
        key !== '%' &&
        key !== '<=' &&
        key !== '±' &&
        key !== 'sin' &&
        key !== 'cos' &&
        key !== 'tan' &&
        key !== 'log' &&
        key !== 'ln' &&
        key !== 'x^' &&
        key !== 'x !' &&
        key !== 'π' &&
        key !== 'e' &&
        key !== 'rad' &&
        key !== '∘'
      ) {
        that.current += key
      } else if (key === '=') {
        if ((that.current).indexOf('^') > -1) {
          let base = (that.current).slice(0, (that.current).indexOf('^'))
          let exponent = (that.current).slice((that.current).indexOf('^') + 1)
          that.current = eval('Math.pow(' + base + ',' + exponent + ')')
        } else {
          that.current = eval(that.current)
        }
      } else if (key === 'C') {
        that.current = ''
      } else if (key === '*') {
        that.current += '*'
      } else if (key === '/') {
        that.current += '/'
      } else if (key === '+') {
        that.current += '+'
      } else if (key === '-') {
        that.current += '-'
      } else if (key === '±') {
        if ((that.current).charAt(0) === '-') {
          that.current = (that.current).slice(1)
        } else {
          that.current += '-' + that.current
        }
      } else if (key === '<=') {
        that.current = that.current.substring(0, that.substring.length - 1)
      } else if (key === '%') {
        that.current = that.current / 100
      } else if (key === 'π') {
        that.current = that.current * Math.PI
      } else if (key === 'x ²') {
        that.current = eval(that.current * that.current)
      } else if (key === '√') {
        that.current = Math.sqrt(that.current)
      } else if (key === 'sin') {
        that.current = Math.sin(that.current)
      } else if (key === 'cos') {
        that.current = Math.cos(that.current)
      } else if (key === 'tan') {
        that.current = Math.tan(that.current)
      } else if (key === 'log') {
        that.current = Math.log10(that.current)
      } else if (key === 'ln') {
        that.current = Math.log(that.current)
      } else if (key === 'x^') {
        that.current += '^'
      } else if (key === 'x !') {
        if (that.current === 0) {
          that.current = '1'
        } else if (that.current < 0) {
          that.current = NaN
        } else {
          let number = 1
          for (let i = that.current; i > 0; i--) {
            number *= i
          }
          that.current = number
        }
      } else if (key === 'e') {
        that.current = Math.exp(that.current)
      } else if (key === 'rad') {
        that.current = that.current * (Math.PI / 180)
      } else if (key === '∘') {
        that.current = that.current * (180 / Math.PI)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
  .calculator
    width 440px
    padding 20px
    border-radius 5px
    margin auto
    font-size 16px
    background hsl(0,0%,20%)
  .input
    width 420px
    height 50px
    padding 0 5px
    margin 0 0 10px 0
    font-size 30px
    border-radius 0
    border 1px solid hsl(0,0%,0%)
    background rgb(51,51,51)
    color #e9e9e9
    outline none
    &:focus,&:active
      border-color rgba(0,0,0,.8)
      box-shadow 0 0 10px 0 rgba(0,0,0,.8)
  .btn
    margin 3px
    width 63px
    border 1px solid hsl(0,0,5%)
    line-height 30px
    border-radius 4px
    color hsl(0,0,80%)
    background hsl(0,0,10%)
    cursor pointer
    outline none
  .lang-btn
    width 136px
  .mode
    display flex
    flex-wrap wrap
    justify-content space-evenly
  .toggle-btn
    border none
    background transparent
    color hsl(0,0,80%)
    width 100%
    cursor pointer
    outline none
    text-shadow 0 0 16px rgb(255,255,255)
    p
      margin 10px 0
</style>
