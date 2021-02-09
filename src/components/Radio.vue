<template>
 <div>
    <p>
      問題 : {{ htmlDecode(q_set.question) }}
    </p>
    <b-form-group  v-slot="{ ariaDescribedby }">
      <b-form-radio v-for="(item,index) in q_set.answers[0]" :key="index"
      @change="selected_action(item)"
      :value="item"
      :aria-describedby="ariaDescribedby"
      name="some-radios"
      :class="this_is_correct_hatena(item)"
      >{{ item  }}</b-form-radio>
    </b-form-group>

    <div class="mt-3">Selected: <strong>{{ selected }}</strong></div>
  </div>
</template>
<style scoped>
    .this_is_correct{
        color: #00008b;
        font-weight: bolder;
    }
</style>
<script>
 import _ from 'lodash'
    export default {
      name: 'Radio',
      props: {
        msg: Object,
        prop_answered: Boolean
    },
    data(){
        return {
            selected_ans_index:-1,
            q_set:{},
            selected:"",
            correct_answer:"",
            is_correct:false,
            tmp:""
        }
    },
      watch: {
 msg:{
    handler(){
        this.q_set.question = this.msg.question;
        this.q_set.answers = [this.shuffleAnswers()];
        this.q_set.correct_answer = this.msg.correct_answer;
                    this.$forceUpdate();
    },
     immediate: true
    }
  }
  ,
    methods:{
        selected_action(item){
            this.selected = item;
            const vm = this;
            //selectedを送る
            vm.$emit('val_changed', this.selected);
        },
        htmlDecode(input){
          var e = document.createElement('textarea');
          e.innerHTML = input;
  // handle case of empty input
  return e.childNodes.length === 0 ? "" : e.childNodes[0].nodeValue;
},
shuffleAnswers(){
    let answers = [...this.msg.incorrect_answers,this.msg.correct_answer];
    console.log(answers);
  return _.shuffle(answers);
},
this_is_correct_hatena(value){
    if(this.prop_answered === false){
        return;
    }
    this.tmp = value;
    if(value === this.q_set.correct_answer){
        return 'this_is_correct';
    }else{
        return '';
    }
}
}
}
</script>