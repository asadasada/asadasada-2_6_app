<template>
    <div>
        <div>
           {{ num }}
       </div>

       <Radio />
       <div v-text=Piyo>

       </div>
   </div>
</template>
<script>
    import Radio from './Radio.vue'
    export default {
  name: 'Piyoko',
  components:{
    Radio
  },
  props: {
    msg: String
  },
  data(){
    return{
        Piyo:"mamama",
        num:0
    }
  },
  methods:{
    testfunc: function(){
        this.num+=1
    }

  }
}
</script>