<template>
<div class="answer_container">
  <b-jumbotron>
    <template #lead>
      コンピュータの学習用のクイズ集です
    </template>

    <hr class="my-4">

    <!-- ここでスロットを使いたい -->
    <Radio v-if="questions.length" :msg="questions[index]" :prop_answered="answered" @val_changed="val_change"
    :key="forceRender_key"
     />
    <b-button variant="primary" href="#" @click="answered_action">submit</b-button>
    <b-button variant="success" href="#" @click="i_increment">Next</b-button>
  </b-jumbotron>
  <b v-if="result.length === 20">あなたが正解したのは{{reslutNum }}問です。</b>
</div>
</template>
<script>
    import Radio from './Radio.vue'
    export default {
  name: 'Answer',
  components:{
    Radio
  },
  props: {
    Ans_prop: String
  },
  data(){
    return{
        index:0,
        questions:[],
        answered:false,
        ans_val:"",
        is_correct:false,
        result:[],
        forceRender_key:0
    }
  },
  methods:{
    i_increment(){
        if(this.index < this.questions.length-1){
            this.index++;
            this.answered=false;
            this.is_correct=false;
            this.forceRender_key+=1;
        }
        if(this.answered === false && this.result.length !== this.questions.length){
            this.result.push(false);
        }
        const vm = this;
        vm.$emit('in_or_de_crement', this.index);
    },
    //
    answered_action(){
        //決め打ち
        if(this.answered || this.result.length === 20){
            return;
        }
        //読みやすいコードを意識する
        this.is_correct = this.questions[this.index].correct_answer === this.ans_val;
        this.result.push(this.is_correct);
        this.answered=true;

    },
    val_change(selected){
        this.ans_val = selected;
    }
  },
  computed:{
    reslutNum(){
        let red = (total,crnt_var)=>{return crnt_var==true ? total+1 : total};
        return this.result.reduce(red,0);
    }
  },
  mounted: function(){
        fetch("https://opentdb.com/api.php?amount=20&category=18&difficulty=medium&type=multiple",{
            method:'GET'}).then(
//results:にarrayで反映
(response)=>{ return(response.json());}
).then((json_data)=>{console.log(json_data);
    this.questions = json_data.results;});
}
}
</script>

