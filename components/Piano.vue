<template>
  <svg :width="20 * 7 * 4" height="100" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <linearGradient id="svg_4" x1="0.410156" y1="0.417969" x2="0.320313" y2="0.144531">
      <stop stop-color="#fff" offset="0"/>
      <stop stop-color="#b7b7b7" stop-opacity="0.996094" offset="1"/>
      </linearGradient>
      <linearGradient id="svg_10" x1="0.558594" y1="0.785156" x2="0.144531" y2="0">
      <stop stop-color="#666666" offset="0"/>
      <stop stop-color="#ffffff" stop-opacity="0.996094" offset="1"/>
      </linearGradient>
    </defs>
    <g v-for="(white, index) in whites" :key="index" :transform="whitePos(index)">
      <rect stroke="#000" id="svg_1" height="100" width="20" x="-0.333333" fill="url(#svg_4)"/>
    </g>
    <g v-for="(black, index) in blacks" :key="index" :transform="blackPos(black)">
      <rect fill="#000000" stroke="#000" width="12" height="60" id="svg_5"/>
      <rect fill="#666666" stroke-width="0" x="11" y="0.333334" width="1" height="59" id="svg_6" stroke="#000"/>
      <rect fill="url(#svg_10)" stroke-width="0" x="0.833333" y="56" width="10.5" height="3.666667" id="svg_8" stroke="#000"/>
    </g>
  </svg>
</template>
<script>

export default {
  data(){
    return {
      whites: [],
      blacks: []
    }
  },
  methods: {
    whitePos(index){
      return `translate(${index * 20},0)`
    },
    blackPos(index){
      return `translate(${index * 20 + 4},0)`
    }
  },
  mounted(){
    for(let i = 0; i < 4; i++){
      this.whites = this.whites.concat([0, 1, 2, 3, 4, 5, 6].map(n => n + 7 * i));
      this.blacks = this.blacks.concat([0.5, 1.5, 3.5, 4.5, 5.5].map(n => n + 7 * i));

    }

  }
}
</script>


