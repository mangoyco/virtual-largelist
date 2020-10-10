<template>
  <LargeList :list="list" v-slot="slotProps">
    <span>{{slotProps.item}}</span>
  </LargeList>
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
</template>

<script>
import LargeList from './components/largeList'
// import * as rrr from 'vue'
const L = []
for (let index = 0; index < 1000; index++) {
  L.push(index)
}

export default {
  name: 'App',
  components: {
    LargeList
  },
  data(){
    return {
      list:L
    }
  },
  mounted(){
  }
}
</script>

<style>
#app {
  height: 500px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
