<template>
  <svg width="400" height="80" @mousemove="over">
    <rect width="200" height="50" rx="8" ry="8" x="20" y="20">
    </rect>
    <text x="120" y="54" text-anchor="middle">I am Button!</text>
    <circle r="10" cx="100" cy="20" class="eye-outer"></circle>
    <circle r="10" cx="130" cy="20" class="eye-outer"></circle>
    <circle r="5" :cx="100 + dx" :cy="20 + dy" class="eye-inner"></circle>
    <circle r="5" :cx="130 + dx" :cy="20 + dy" class="eye-inner"></circle>
  </svg>
</template>
<script lang="ts">
import Vue from "vue"

export default Vue.extend({
  data(){
    return {
      dx: 2,
      dy: 2
    }
  },
  methods: {
    over(ev: MouseEvent){
      const cx = 100
      const cy = 20
      const dx = ev.offsetX - cx
      const dy = ev.offsetY - cy
      this.dx = dx / 400 * 4
      this.dy = dy / 80 * 4
    }
  }
})
</script>
<style scoped>
rect{
  fill: white;
  stroke: #793;
  stroke-width: 5px;
  cursor: pointer;
}
rect:hover{
  fill: #EFE;
}

.eye-outer{
  fill: white;
  stroke: #793;
  stroke-width: 5px;
}
text{
  cursor: pointer;
  pointer-events: none;
}

.eye-inner{
  fill: #793;
}
</style>
