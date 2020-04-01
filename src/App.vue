<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <button @click="next">next</button>
    <div class="outer">
      <TextSlide
        :txt="text"
        :styles="{background: 'red', height:'2em', width: '2em', borderRadius: '1em'}"
        :styles-inner="{color: 'white', alignItems:'center', justifyContent:'center'}"
        distanceX="50%"
        data-key="b"
      />
    </div>
  </div>
</template>

<script>
import TextSlide from "./components/TextSlide";

const TEXTS = [
  '0',
  '11',
  '222',
  '33',
  '444',
]

export default {
  name: 'App',
  components: {
    TextSlide
  },
  data () {
    return {
      text: '',
      i: 0,
      TEXTS,
    }
  },
  mounted() {
    this.next()
  },
  methods: {
    next() {
      this.i = this.getIndex()
      this.text = TEXTS[this.i]
    },
    getIndex() {
      const newIndex = this.i === (TEXTS.length - 1) 
        ? 0
        : this.i + 1
      return newIndex
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
