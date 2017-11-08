<template>
  <div id="app">
    <piano></piano>
    <cute-button></cute-button>
    <sparkline></sparkline>
    <slider></slider>
  </div>
</template>

<script>
import CuteButton from "./CuteButton.vue"
import Sparkline from "./Sparkline.vue"
import Slider from "./Slider.vue"
import Piano from "./Piano.vue"
export default {
  name: 'app',
  data () {
    return {
    }
  },
  components: {
    CuteButton,
    Sparkline,
    Slider,
    Piano
  }
}
</script>

<style>
body{
  background: #EFE;
  margin-top: 5rem;
  text-align: center;
}

</style>
