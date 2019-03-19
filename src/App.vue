<template>
  <div id="app">
    <start v-if='page === 1' @start='start'></start>
    <game v-if='page === 2' @reStart='reStart'></game>
  </div>
</template>

<script>
import start from './components/start.vue'
import game from './components/game.vue'


export default {
  name: 'app',
  components: {
    start,
    game
  },
  data(){
    return{
      page:1,
    }
  },
  methods:{
    start(){
      this.page = 2
    },
    reStart(){
      this.page = 1
    }
  }
}
</script>

<style>
Html,body{
  margin: 0;
  padding: 0;
  font-family: "Roboto Condensed", Arial, sans-serif;
}
*{
  box-sizing: border-box;
}
#app{
  width: 100%;
  height: 100%;
  min-height: 100vh
}
</style>
