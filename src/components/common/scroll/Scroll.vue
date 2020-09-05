<template>
   <div ref="wrapper">
       <div class="content">
           <slot></slot>
       </div>
   </div>
</template>

<script>
import BScroll from 'better-scroll'

export default {
  name: "Scroll",
  data(){
      return {
          scroll:null
      }
  },
  mounted(){
      this.scroll = new BScroll(this.$refs.wrapper, {
      probeType: 3,
    //   pullUpLoad: true
    })
    this.scroll.on('scroll',(position) => {
      console.log(position);
    })
  }
}
</script>

<style>

</style>