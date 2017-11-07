<template>
  <div id="app">
    <cute-button></cute-button>
    <sparkline></sparkline>
  </div>
</template>

<script>
import CuteButton from "./CuteButton.vue"
import Sparkline from "./Sparkline.vue"
export default {
  name: 'app',
  data () {
    return {
    }
  },
  components: {
    CuteButton,
    Sparkline
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
