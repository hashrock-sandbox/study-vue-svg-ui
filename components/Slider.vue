<template>
<svg
   version="1.1"
   viewBox="0 0 400 100"
   height="100"
   width="400" @pointermove="onDrag" @pointerup="stopDrag" @pointerover="over" @pointerout="out">
  <g
     id="layer1">
    <path
       id="backline"
       d="M 47.669515,50 H 370"
       style="fill:none;fill-rule:evenodd;stroke:#668000;stroke-width:4;stroke-linecap:butt;stroke-linejoin:miter;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
    <g
       style="stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none"
       transform="matrix(3.5831086,0,0,3.5831086,18.212845,-966.44304)"
       id="chara" :transform="charaPosition" @pointerdown="startDrag">
      <g
         style="stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none"
         id="dragpoint">
        <circle
           r="6.614583"
           cy="283.8653"
           cx="8.2209845"
           id="path4489"
           style="opacity:1;fill:#ffffff;fill-opacity:0.4073171;stroke:#668000;stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
      </g>
      <g
         style="stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none"
         id="eyes" v-show="letsmove">
        <circle
           r="2.4201274"
           cy="277.2507"
           cx="5.8208332"
           id="path4508"
           style="opacity:1;fill:#ffffff;fill-opacity:0.92439025;stroke:#668000;stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
        <circle
           r="2.4201274"
           cy="277.2507"
           cx="10.734524"
           id="path4508-2"
           style="opacity:1;fill:#ffffff;fill-opacity:0.92439025;stroke:#668000;stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
        <circle
           r="0.66145831"
           cy="277.25073"
           cx="5.8208332"
           id="path4525"
           style="opacity:1;fill:#668000;fill-opacity:1;stroke:none;stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
        <circle
           r="0.66145831"
           cy="277.15622"
           cx="10.829018"
           id="path4525-6"
           style="opacity:1;fill:#668000;fill-opacity:1;stroke:none;stroke-width:1.11634908;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
      </g>
    </g>
  </g>
</svg>
</template>
<script>

function scale(val){
  return 18 + (341 - 18) * val / 100
}
function invert(x){
  return (100 * x - 18) / (341-18)
}

export default {
  data(){
    return {
      val: 50,
      offset: 0,
      drag: false,
      letsmove: true
    }
  },
  computed:{
    charaPosition(){
      const x = scale(this.val)
      return `matrix(3.5831086,0,0,3.5831086,${x},-966.44304)`
    }
  },
  methods:{
    startDrag(e){
      this.drag = true
      this.offset = e.offsetX - scale(this.val)
    },
    onDrag(e){
      if(this.drag){
        this.val = invert(e.offsetX - this.offset)
        if(this.val > 100){
          this.val = 100
        }
        if(this.val < 0){
          this.val = 0
        }
      }
    },
    stopDrag(e){
      this.drag = false
      this.offset = 0
    },
    over(){
      this.letsmove = false;
    },
    out(){
      this.letsmove = true;
    }
  },
  mounted(){
    setInterval(()=>{
      if(this.val && this.letsmove){
        if(this.val > 48){
          this.val -= 1
        }
        if(this.val < 52){
          this.val += 1
        }
      }
    }, 200)
  }
}
</script>
