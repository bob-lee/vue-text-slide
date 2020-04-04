<template>
  <div 
    class="bl-animate-value-box"
    :data-key="dataKey"
  >
    <div 
      class="inner enter-base-js"
    >
      <div class="box">
        {{ enterText }}
      </div>
    </div>
    <div 
      class="inner leave-base-js"
    >
      <div class="box">
        {{ leaveText }}
      </div>
    </div>
  </div>
</template>

<script>
const ENTER_DIV = '.enter-base-js'
const LEAVE_DIV = '.leave-base-js'
const DISTANCE_X = '5%'

export default {
  name: "TextSlide",
  props: {
    txt: String,
    dataKey: {
      type: String,
      required: false,
      default: 'default'
    },
    distanceX: {
      type: String,
      required: false,
    },
    styles: {
      type: Object,
      required: false,
    },
    stylesInner: {
      type: Object,
      required: false,
    }
  },
  data () {
    return {
      container: null,
      inner: null,
      entered: false, // if true, enterDiv is entered
                      // if false, enterDiv is to enter
      enterText: '',
      leaveText: '',
      enterDiv: null,
      leaveDiv: null,
      offsetHeight: null,
    }
  },
  watch: {
    txt(v) {
      this.showNew(v)
    },
  },
  mounted() {
    this.container = document.querySelector(`[data-key=${this.dataKey}].bl-animate-value-box`)
    this.inners = this.container.querySelectorAll('.inner')
    if (this.styles) {
      Object.keys(this.styles).forEach(x => {
        this.container.style[x] = this.styles[x]
      })
    }
    if (this.stylesInner) {
      Object.keys(this.stylesInner).forEach(x => {
        this.inners.forEach(y => y.style[x] = this.stylesInner[x])
      })
    }
    this.enterDiv = this.container.querySelector(ENTER_DIV)
    this.leaveDiv = this.container.querySelector(LEAVE_DIV)
    this.enterDiv.style.transform = `translateX(-${this.distanceX || DISTANCE_X})`
    this.leaveDiv.style.transform = "translateX(0)"
    this.enterDiv.style.opacity="0"
    this.leaveDiv.style.opacity="1"

    this.enterDiv.addEventListener('transitionend', this.enterEnd);
  },
  beforeDestroy() {
    this.enterDiv.removeEventListener('transitionend', this.enterEnd);
  },
  methods: {
    apply(styles) {
      if (styles) {
        Object.keys(styles).forEach(x => {
          this.container.style[x] = styles[x]
        })
      }
    },
    applyInner(styles) {
      if (styles) {
        Object.keys(styles).forEach(x => {
          this.inner.style[x] = styles[x]
        })
      }
    },
    showNew(text) {
      if (this.entered) {
        this.leaveText = text
        this.enterDiv.style.transform = `translateX(${this.distanceX || DISTANCE_X})`
        this.leaveDiv.style.transform = "translateX(0)"
        this.enterDiv.style.opacity="0"
        this.leaveDiv.style.opacity="1"
      } else {
        this.enterText = text
        this.enterDiv.style.transform = "translateX(0)"
        this.leaveDiv.style.transform = `translateX(${this.distanceX || DISTANCE_X})`
        this.enterDiv.style.opacity="1"
        this.leaveDiv.style.opacity="0"
      }
      this.entered = !this.entered
    },
    enterEnd() {
      if (this.entered) {
        this.leaveDiv.classList.add('notransition');
        this.leaveDiv.style.transform = `translateX(-${this.distanceX || DISTANCE_X})`
        this.offsetHeight = this.leaveDiv.offsetHeight
        this.leaveDiv.classList.remove('notransition');
      } else {
        this.enterDiv.classList.add('notransition');
        this.enterDiv.style.transform = `translateX(-${this.distanceX || DISTANCE_X})`
        this.offsetHeight = this.enterDiv.offsetHeight
        this.enterDiv.classList.remove('notransition');
      }
    },

  },

};
</script>

<style scoped>
.bl-animate-value-box {
  display: inline-block;
  position: relative;
  height: 1.5em;
  width: 35em;
  font-size: 1rem;
  font-weight: 300;
}
.bl-animate-value-box .inner {
  position: absolute;
  height: 100%;
  width: 100%;
  display: flex;
  justify-content: flex-start;
  transition-property: transform, opacity;
  transition-duration: .2s;
  transition-timing-function: ease-out;
}
.notransition {
  -webkit-transition: none !important;
  -moz-transition: none !important;
  -o-transition: none !important;
  transition: none !important;
}
.dev {
  border: 1px blue solid;
}
</style>
