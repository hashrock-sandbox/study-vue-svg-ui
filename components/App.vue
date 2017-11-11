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

<script lang="ts">
import Vue from "vue"

import CuteButton from "./CuteButton.vue"
import Sparkline from "./Sparkline.vue"
import Slider from "./Slider.vue"
import Piano from "./Piano.vue"
import Spin from "./Spin.vue"

export default Vue.extend({
  name: 'app',
  data () {
    return {
      msg: ""
    }
  },
  components: {
    CuteButton,
    Sparkline,
    Slider,
    Piano,
    Spin
  },
  methods: {
    test(){
    }
  }

})
</script>

<style>
body{
  background: #EFE;
  margin-top: 5rem;
  text-align: center;
}

</style>
