<template>
  
  <!-- <div class="start" :class="{ end : 모달창열렸니}">
    <Modal @closeModal="모달창열렸니=false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
  </div> -->

  <transition name="fade">
    <Modal @closeModal="모달창열렸니=false" :원룸들="원룸들" :누른거="누른거" :모달창열렸니="모달창열렸니" />
  </transition>

  <div class="menu">
    <a v-for="작명 in menu" :key="작명">{{ 작명 }}</a>
  </div>

  <Discount v-if="showDiscount==true" :할인율="할인율"/>

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">되돌리기</button>
  <!-- <div v-for="방,i in products" :key="방">
    <img :src="require('./assets/room'+i+'.jpg')"> 원래 되는것
    <img :src="`./assets/room${i}.jpg`"> 이번에 새로 질문한것
    <h4>{{방}}</h4>
    <p>{{price1+i*10}} 만원</p>
    <button @click="신고수[i]++">허위매물신고</button>
    <span>신고수 : {{신고수[i]}}</span>
  </div> -->
  
  <Card @openModal="모달창열렸니=true; 누른거=$event" :원룸들="원룸들[i]" :모달창열렸니="모달창열렸니"  v-for="(a,i) in 원룸들" :key="i"/>
 
</template>

<script>
import data from './assets/oneroom.js';
import Discount from './assets/Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue';


export default {
  name: 'App',
  data(){
    return {
      몸틈새넣기 : 0,
      showDiscount : true,
      오브젝트 : {name : 'kim', age : 20},
      누른거 : 0,
      원룸들 : data,
      원룸들오리지널: [...data],
      모달창열렸니 : false,
      신고수 : [0,0,0],
      price1 : 60,
      price2 : 70,
      price3 : 80,
      menu:['Home','Shop','About'],
      products :['역삼동원롬','천호동원룸','마포구원룸'],
      할인율 : 30,
    }
  },
  methods : {
    increase(){
      this.신고수++;
    },
    priceSort(){
      this.원룸들.sort(function(a,b){
        return a.price-b.price;
      })
    },
    sortBack(){
      this.원룸들=[...this.원룸들오리지널];
    },
  },
  // mounted(){
  //   setTimeout(()=>{
  //     this.showDiscount=false;
  //   },2000);
  // },
  mounted(){
    setInterval(()=>{
      this.할인율--;
      if(this.할인율==0)
      {
        this.showDiscount=false;
      }
    },1000);
  },
  components: {
    Discount : Discount,
    Modal : Modal,
    Card : Card,
  }
}
</script>

<style>
.fade-enter-from {
  opacity : 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity : 1;
}

/* .start{
  opacity: 0;
  transition: all 1s;
}
.end{
  opacity: 1;
} */

body{
  margin : 0
}
div{
  box-sizing: border-box;
}
.black-bg{
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding:20px;
}
.white-bg{
  width : 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.menu{
  background: darkslateblue;
  padding:15px;
  border-radius: 5px;
}
.menu a{
  color : white;
  padding:10px;
}
.room-img{
  width : 60%;
  margin-top:40px;
}
.discount{
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
</style>
