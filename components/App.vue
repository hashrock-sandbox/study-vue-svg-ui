<template>
  <div id="app">
    <cute-button></cute-button>
    <sparkline></sparkline>
    <slider></slider>
  </div>
</template>

<script>
import CuteButton from "./CuteButton.vue"
import Sparkline from "./Sparkline.vue"
import Slider from "./Slider.vue"
export default {
  name: 'app',
  data () {
    return {
    }
  },
  components: {
    CuteButton,
    Sparkline,
    Slider
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
