<template>
  <div id="app">
    <Header :index="index"/>
    <div class="container">
  <div class="row">
    <div class="col-3 offset-3">
      <!-- Content -->
    </div>
  </div>
  <!-- This class can be used with responsive classes such as -md- as well: -->
  <div class="row">
    <div class="col-md-6 offset-md-3">
      <Answer @in_or_de_crement="fix_index" />
    </div>
  </div>
</div>
  </div>
</template>

<script>
import Answer from './components/Answer.vue'
import Header from './components/Header.vue'
export default {
  name: 'App',
  components: {
    Answer,Header
  },
  data(){
    return{
        test:"unko",
        index:0
    }
  },
  methods:{
    fix_index: function(i){
        this.index = i;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
