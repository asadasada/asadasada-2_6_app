<template>
<div>
  <b-nav>
    <b-nav-item disabled><b>コンピュータのクイズ</b></b-nav-item>
    <b-nav-item disabled><b>{{ index+1 }}/20</b></b-nav-item>
  </b-nav>
</div>
</template>
<script>
    export default{
          name: 'Header',
          props:{
            //予約語は使わない様にする
            index:Number
          }
    }

</script>