<template>
  <div ref="list" class="list_outer" @scroll="onscroll($event)">
    <div class="heightholder" :style="{ height: listHeight + 'px' }"></div>
    <div class="real_list" :style="{ transform: getTransform }">
      <div class="test" v-for="(item,index) in realList" :key="index">{{item}}</div>
    </div>
  </div>
  <!-- <div>{{num}}</div> -->
</template>
<script>
import {setup,onMounted, reactive,ref,computed,getCurrentInstance}from 'vue'
export default{
  props: {
    list: Array,
    default:()=>[]
  },
  setup({list}){
    let startindex = ref(0)
    let endindex = computed(()=> startindex.value + 10)
    let realList = computed(()=>list.slice(startindex.value,Math.min(endindex.value,list.length)))
    let getTransform = computed(()=> `translate3d(0,${transY.value}px,0)`)

    const listHeight = 60 * list.length
    const transY = ref(0)
    const {ctx} = getCurrentInstance()
    function onscroll(e){
      let scrollTop = ctx.$refs.list.scrollTop;
      startindex.value = Math.floor(scrollTop / 120) * 2; // 隐藏两个的话乘以2，无意义，就是加深下理解....
      transY.value = scrollTop - (scrollTop % 120);
      console.log(scrollTop)
      console.log(scrollTop % 60)
    }
    
    return { 
      realList,
      listHeight,
      onscroll,
      getTransform
    }
  }
}
</script>
<style scoped>
.list_outer{
  width: 100%;
  height: 100%;
  overflow-y: auto;
  position: relative;
}
.list_outer .heightholder{
  width: 100%;
  position: absolute;
}
.test{
  height: 60px;
  border-bottom: 1px solid black;
}
</style>