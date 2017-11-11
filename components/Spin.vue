<template>
  <svg width="100" height="100" @mousedown="click">
    <line v-for="(line, idx) in lines"
      :key="idx"
      :x1="toPos(line).x1"
      :x2="toPos(line).x2"
      :y1="toPos(line).y1"
      :y2="toPos(line).y2"
      :stroke="toPos(line).color"
    ></line>

  </svg>
</template>
<script lang="ts">
import Vue from "vue"

interface Line{
  x1: number
  x2: number
  y1: number
  y2: number
  color: string
}

export default Vue.extend({
  data(){
    return {
      lines: <number[]>[],
      t: 0,
      d: 0.005,
      l: 15,
      m: false,
      dy: 0,
      ay: 0
    }
  },
  methods:{
    click(){
      if(!this.m){
        this.d += 0.01;
        this.ay = -2
      }
    },
    toPos(i: number): Line{
      const cx = 50;
      const cy = 50 + this.dy;
      const l2 = 30;
      const l1 = l2 - this.l;
      let a = 2 * 3.1415 * i / 16
      let c = Math.floor((i/16 + this.t)*255) % 255
      return {
        x1: Math.cos(a) * l1 + cx,
        y1: Math.sin(a) * l1 + cy,
        x2: Math.cos(a) * l2 + cx,
        y2: Math.sin(a) * l2 + cy,
        color: this.m ? "red" : `rgb(${c},${c},${c})`
      }
    }
  },
  mounted(){
    for(let i = 0; i < 16; i++){
      this.lines.push(i)
    }

    let t = 0
    setInterval(()=>{
      this.t += this.d;
      if(this.t > 1){
        this.t = 0;
      }
      this.dy += this.ay
      this.ay += 0.6
      if(this.dy > 0){
        this.dy = 0;
      }

      if(this.d > 0.1){
        this.m = true
        this.l = this.l * 0.9
      }
    }, 10)

  }
})
</script>
<style scoped>
line{
  fill: black;
  stroke-width: 4px;
}
svg{
  cursor: pointer;
}
</style>
