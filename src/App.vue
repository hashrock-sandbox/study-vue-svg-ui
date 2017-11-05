<template>
  <div id="app">
    <cute-button></cute-button>
  </div>
</template>

<script>
import CuteButton from "./CuteButton.vue"
export default {
  name: 'app',
  data () {
    return {
    }
  },
  components: {
    CuteButton
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
