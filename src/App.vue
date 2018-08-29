<template>
  <div id="app">
    <lottie id="loader" :options="defaultOptions" :height="84" :width="84"
            v-on:animCreated="handleAnimation" v-bind:class="{ hidden: isHidden }" />
    <button v-on:click="exitLoop">exit loop</button>
  </div>
</template>

<script>
  import Lottie from './lottie.vue'
  import * as animationData from './assets/logo_loading.json'
  import * as breakpoints from './assets/breakpoints.json'

  export default {
    name: 'app',
    components: {
      'lottie': Lottie
    },
    data () {
      return {
        defaultOptions: {animationData: animationData},
        isHidden: false
      }
    },
    methods: {
      handleAnimation: function (anim) {
        this.anim = anim
        this.anim.setSpeed(1.1)
        this.anim.playSegments(breakpoints.loop, true)
      },

      stop: function () {
        this.anim.stop()
      },

      play: function () {
        this.anim.play()
      },

      pause: function () {
        this.anim.pause()
      },

      exitLoop: function () {
        this.anim.loop = false
        this.anim.playSegments(breakpoints.end, false)
        this.anim.addEventListener('complete', this.fadeAway)
      },

      fadeAway: function () {
        console.log('FADE AWAY')
        this.isHidden = true
      }
    }
  }
</script>

<style>
body {
  height: 100%;
  width: 100%;
  background: 
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: absolute;
  height: 100%;
  width: 100%;
  top: 50%;
  /* adjust top up half the height*/
  margin-top: -6em;
}
.hidden {
  visibility: hidden;
  opacity: 0;
  transition: all 1200ms cubic-bezier(0.230, 1.000, 0.320, 1.000); /* easeOutQuint */
}
</style>
