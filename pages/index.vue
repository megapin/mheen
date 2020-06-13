<template>
  <v-layout justify-start column>

    <v-flex>
      <no-ssr>
        <vue-typer text="민 인터랙트"
          :repeat='Infinity'
          :shuffle='true'
          initial-action='typing'
          :pre-type-delay='70'
          :type-delay='150'
          :pre-erase-delay='2000'
          :erase-delay='250'
          erase-style='backspace'
          :erase-on-complete='true'
          caret-animation='expand'
        ></vue-typer>
      </no-ssr>
    </v-flex>

    <!-- <v-flex>
      <div class="bubble-wrapper">
        <div ref="bubble" class="bubble">
          <img :src="curLogo" class="bubble-image">
        </div>
        <div ref="bubblePulse" class="bubble-pulse"></div>
      </div>
    </v-flex> -->
    
  </v-layout>
</template>

<script>
// let TimelineLite
import {TimelineLine, Back, Elastic, Expo} from 'gsap'

if (process.browser) {
  var VueTyper = require('vue-typer').VueTyper
  // TimelineLite = require('gsap')
}

export default {
  components: {
    VueTyper
  },
  data() {
    return {
      timeline: null,
      logos: [
        'iconmonstr-slack-6.svg', 
        'iconmonstr-android-os-4.svg', 
        'iconmonstr-facebook-5.svg', 
        'iconmonstr-twitter-4.svg'
      ],
      curLogo: ''
    }
  },
  methods: {
    randomiseLogo() {
      const logosToSample = this.logos.filter(logo => logo !== this.curLogo)
      this.curLogo = logosToSample[Math.floor(Math.random() * logosToSample.length)]
    }
  },
  mounted() {
    this.randomiseLogo() 

    const {bubble, bubblePulse} = this.$refs

    this.timeline = new TimelineLite({
      onComplete: () => {
        this.randomiseLogo()
        this.timeline.restart()
      }
    })

    // timeline.to(box, 1, {x: 200, rotation: 90, ease: Back.easeInOut})
    // timeline.to(box, 0.5, {background: 'white'}, '-=0.5')

    // timeline.to(bubble, 0.4, {
    this.timeline.to(bubble, 0.4, {
      scale: 0.8,
      rotation: 16,
      ease: Back.easeOut.config(1.7)
    })
    // timeline.to(bubblePulse, 0.5, {
    this.timeline.to(bubblePulse, 0.5, {
      scale: 0.9,
      opacity: 1
    }, '-=0.6')

    this.timeline.to(bubble, 1.2, {
    // timeline.to(bubble, 1.2, {
      scale: 1,
      rotation:'-=16',
      ease: Elastic.easeOut.config(2.5, 0.5)
    })
    this.timeline.to(bubblePulse, 1.1, {
    // timeline.to(bubblePulse, 1.1, {
      scale: 3,
      opacity: 0,
      ease: Expo.easeOut
    }, '-=1.2')
  }
}
</script>

<style>
.bubble-wrapper {
  position: relative;
}
.bubble{
  position: relative;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid white;
  background: wheat;
  border-radius: 50%;
  height: 100px;
  width: 100px;
}
.bubble-pulse {
  position: absolute;
  z-index: 1;
  height: 120px;
  width: 120px;
  top: 50%;
  left: 50%;
  margin-top: -60px;
  margin-left: -60px;
  background: wheat;
  border-radius: 50%;
  opacity: 0;
  transform: scale(0);
}
.bubble-image {
  height: 50%;
  /* background-color: wheat; */
}
.box {
  height: 50px;
  width: 50px;
  background: blue;
}
.vue-typer {
  font-family: Copperplate, 'Copperplate Gothic Light', fantasy;
}
.vue-typer .custom.char.typed {
  color: white;
  font-size: 4.5em;
}
.vue-typer .custom.char.selected {
  color: white;
  /* font-size: 8em; */
  background-color: transparent;
  /* text-decoration: line-through; */
}
.vue-typer .custom.caret {
  /* display: none; */
  color: yellow;
}
</style>
