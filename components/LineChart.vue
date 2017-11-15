<template>
  <div>
  <svg width="300" height="100" @wheel="wheel" @pointerdown="startDrag" @pointermove="onDrag" @pointerup="stopDrag">
    <polyline fill="none" stroke="#793" :points="points"></polyline>
  </svg>
  <div>
    center: <input type="range" min="0" max="100" v-model="cx">
    zoom: <input type="range" min="0.05" max="1" step="0.05" v-model="zoom">
  </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import * as scale from "d3-scale"

const scaleproto =  scale.scaleLinear()
let scalefn: scale.ScaleLinear<number, number>

export default Vue.extend({
  data() {
    return {
      dat: <number[]>[],
      cx: "150",
      zoom: 1,
      drag: false,
      offset: 0,
      move: 0
    };
  },
  computed: {
    x1(): number{
      return parseFloat(this.cx) - this.zoom * 75
    },
    x2(): number{
      return parseFloat(this.cx) + this.zoom * 75
    },
    points(): string {
      scalefn = scaleproto.domain([this.x1, this.x2]).range([0, 300])
      return `${scalefn(0)},100 ` + this.dat
        .map((item: number, i: number) => {
          return `${scalefn(i)},${item}`;
        })
        .join(" ") + ` ${scalefn(300)}, 100`;
    }
  },
  methods: {
    wheel(event: MouseWheelEvent){
      this.zoom += event.deltaY * (event.deltaMode ? 120 : 1) / 500;
      if(this.zoom <= 0){
        this.zoom = 0.05
      }
    },
    startDrag(e: PointerEvent){
      this.drag = true
      this.offset = e.offsetX
    },
    onDrag(e: PointerEvent){
      if(this.drag){
        this.move = (this.offset - e.offsetX) * this.zoom / 2
        this.offset = e.offsetX
        this.cx = (parseFloat(this.cx) + this.move).toString()
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
        (Math.random() + Math.random() + Math.random() + Math.random()) / 4 * 100
      );
    }
    scalefn = scaleproto.domain([0, 20]).range([0, 300])
  }
});
</script>
<style scoped>
svg{
  background: white;
  cursor: -webkit-grab; 
}
polyline{
  fill: #e7ece7;
}
</style>
