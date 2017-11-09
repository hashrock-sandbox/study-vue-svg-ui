<template>
  <div id="app">
    <div>
      <spin></spin>
    </div>
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
import Spin from "./Spin.vue"

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
    Piano,
    Spin
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
