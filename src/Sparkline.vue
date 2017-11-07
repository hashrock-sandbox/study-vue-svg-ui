<template>
  <svg width="300" height="50">
    <polyline fill="none" stroke="#793" :points="points"></polyline>
  </svg>  
</template>

<script>
export default {
  data(){
    return {
      dat: []
    }
  },
  computed:{
    points(){
      return this.dat.map((item, i)=>{
        return `${i},${item}`
      }).join(" ")
    }
  },
  mounted(){
    //ランダムデータ
    for(let i =0; i < 300; i++){
      this.dat.push(
        (Math.random() + Math.random() + Math.random() + Math.random()) / 4 * 50
      )
    }
  }

}
</script>
