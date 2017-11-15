<template>
  <svg :width="w" :height="h" @wheel="wheel" @pointerdown="startDrag" @pointermove="onDrag" @pointerup="stopDrag">
    <polyline fill="none" stroke="#793" :points="points"></polyline>
    <line class="grid" v-for="(tick, index) in ticks" :key="index" :x1="scaleTick(tick)" :y1="0" :x2="scaleTick(tick)" :y2="h"></line>
  </svg>
</template>

<script lang="ts">
import Vue from "vue";
import * as scale from "d3-scale"

const scaleproto =  scale.scaleLinear()
let scalefn: scale.ScaleLinear<number, number>

export default Vue.extend({
  data() {
    return {
      w: 400,
      h: 200,
      dat: <number[]>[],
      cx: 150,
      zoom: 2,
      drag: false,
      offset: 0,
      move: 0,
      ticks: <number[]>[]
    };
  },
  computed: {
    x1(): number{
      return this.cx - 150 / this.zoom
    },
    x2(): number{
      return this.cx + 150 / this.zoom
    },
    points(): string {
      scalefn = scaleproto.domain([this.x1, this.x2]).range([0, this.w])
      this.ticks = scalefn.ticks(5)
      return `${scalefn(0)},${this.h} ` + this.dat
        .map((item: number, i: number) => {
          return `${scalefn(i)},${item}`;
        })
        .join(" ") + ` ${scalefn(300)}, ${this.h}`;
    }
  },
  methods: {
    wheel(event: MouseWheelEvent){
      this.zoom = this.zoom + -event.deltaY * (event.deltaMode ? 120 : 1) / 500
      if(this.zoom <= 0){
        this.zoom = 0.05
      }
    },
    scaleTick(x: number){
      return scalefn(x)
    },
    startDrag(e: PointerEvent){
      this.drag = true
      this.offset = e.offsetX
    },
    onDrag(e: PointerEvent){
      if(this.drag){
        this.move = (this.offset - e.offsetX) / this.zoom
        this.offset = e.offsetX
        this.cx = this.cx + this.move
      }
    },
    stopDrag(e: PointerEvent){
      this.drag = false
      this.offset = 0
    },    
  },
  mounted() {
    //ランダムデータ
    for (let i = 0; i < 300; i++) {
      this.dat.push(
        (Math.random() + Math.random() + Math.random() + Math.random()) / 4 * this.h
      );
    }
    scalefn = scaleproto.domain([0, 20]).range([0, this.w])
  }
});
</script>
<style scoped>
svg{
  background: white;
  cursor: normal; 
}
polyline{
  fill: #e7ece7;
}
.grid{
  stroke: #d5ded5;
}

</style>
