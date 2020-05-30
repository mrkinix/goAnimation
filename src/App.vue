<template>
  <div id="app">
          <img v-if="visib" class="orange" :src="require('@/assets/portal.png')">
      <img v-if="visib" :src="require('@/assets/portal.png')">
    <div class="o"
    :style="{transform: `translate(${x}vw, ${y}vw)`}"
    ></div>
    <LottieAnimation
    :path="'./' + state + '.json'"
    :loop="auto"
    :autoPlay="true"
    :speed="2"
    :width="200"
    :height="200"
    id="anim"
    :style="{right: pos + 'vw', top: pos2 + 'vh'}"
    />
  </div>
</template>

<script>
import LottieAnimation from '../node_modules/lottie-vuejs/src/LottieAnimation.vue' // import lottie-vuejs
import delay from 'delay'

export default {
  data() {
    return {
      pos: 0,
      state: 'moving',
      auto: true,
      pos2: 50,
      x: 0,
      y: 0,
      visib: false
    }
  },
  components: {
    LottieAnimation
  },
  async mounted() {
    for (let i = 0; i <100; ++i) {
      await delay(17)
      this.pos += .3
    }
    this.state = 'eyeroll'
    this.auto = false
    await delay(1000)
    this.state = 'kick'
    await delay(200)
    for (let i = 0; i <100; ++i) {
      await delay(7)
      this.x += .3 + Math.random() * .2
      this.y -= .3 + Math.random() * .2
    }
    await delay(1000)
    for (let i = 0; i <30; ++i) {
      await delay(7)
      this.pos -= .1
    }
    for (let i = 0; i <30; ++i) {
      await delay(7)
      this.pos2 -= .1
    }
    this.state = 'jump'
    await delay(2000)
    this.visib = true
    this.state = 'data'
    this.auto = true
    for (let i = 0; i <100; ++i) {
      await delay(7)
      this.pos2 += .55
    }
    for (let i = 0; i < 69; ++i) {
      await this.loop()
    }
  },
  methods: {
    loop: async function() {
      this.pos2 = -10;
      for (let i = 0; i <200; ++i) {
        await delay(7)
        this.pos2 += .55
      }
    }
  },
}
</script>

<style>
#app {
  background: black;
  height: 100%;
  width: 100%;
  position: fixed;
  top: 0;
  left:0;
}
#anim {
  position: fixed;
  top: 50vh;
}

.o {
  height: 300px;
  width: 200px;
  background: rgb(65, 59, 59);
  position: fixed;
  top: calc(50% - 130px);
  right: calc(30% - 150px);
}

img {
  position: absolute;
  height: 200px;
  right: 27%;
  bottom: -40px;
  width: auto;
  transform: rotate(90deg);
  filter: hue-rotate(185deg) ;
}

.orange {
  top: -40px;
  filter: hue-rotate(0) ;
}

</style>
