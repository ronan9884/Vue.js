<template>
  <div class="black-bg" v-if="모달창열렸니==true">
    <div class="white-bg">
      <h4>{{원룸들[누른거].title}}</h4>
      <img :src="원룸들[누른거].image" style="width : 50%">
      <p>{{원룸들[누른거].content}}</p>
      <!-- <input @input="month = $event.target.value"> 입력방법 1 -->
      <input v-model="month"> <!--  입력한거 바로 값에 넣어줌-->
      <p> {{month}}개월 선택함 : {{원룸들[누른거].price * month}}원</p>
      <button @click="$emit('closeModal')">닫기</button>
      </div>
  </div>
</template>

<script>


export default {
    name:'Modal',
    data(){
      return{
        month : 1,
      }
    },
    watch : {
      month(a){
        if(isNaN(a)==true || a==' ')
        {
          alert('문자 입력 ㄴ');
          this.month=1;
        }
      }
    },
    props : {
        원룸들 : Array,
        누른거 : Number,
        모달창열렸니 : Boolean,
    },
    beforeUpdate(){
    if(this.month==2){
      alert('2개월은 너무 적소');
    }
  }
}
</script>

<style>

</style>