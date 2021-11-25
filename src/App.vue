<template>
<!-- 애니메이션을 주기 위해서는 시작 / 끝 클래스 2가지를 쓰면 된다/-->
<transition name = "fade">
<Modal :data="data" :누른거="누른거" :모달창열렸니="모달창열렸니" @modal = "모달창열렸니 = false" @modalClose = "modal"></Modal>
</transition>



  <div class="menu">
  <!-- 뷰의 반복문!  -->
  <!-- <a v-for="작명 in 반복횟수 (또는 데이터) :key="작명"></a> -->
  <a v-for="(a , index) in 메뉴들" :key="index">{{ a }}</a>
  </div>


<Discount v-if ="showDiscount" :disCountPercent="disCountPercent"></Discount>

<button @click = "priceSort" >가격 낮은 순 정렬 버튼</button>
<button @click = "priceSortReverse" >가격  높은 순 정렬 버튼</button>
<button @click = "abcSort" >가나다 순서</button>
<button @click = "resetSort" >순서 리셋하기 </button>
<button @click = "filterSort" >50만원이상만</button>


 <Card v-for="(el, index) in data" :key="index" :datum="data[index]" @openModal="모달창열렸니 = true; 누른거 = $event"></Card>
 <!-- <Card :datum="data[0]"></Card>
 <Card :datum="data[1]"></Card>
 <Card :datum="data[2]"></Card>
 <Card :datum="data[3]"></Card>
 <Card :datum="data[4]"></Card>
 <Card :datum="data[5]"></Card> -->



  <!-- <div v-for="(a, index) in data" :key="index">  -->
    <!-- HTML의 속성에 데이터 바인딩을 하고 싶을 때는 colone을 넣어주면 된다! -->
    <!-- <img :src="data[index].image" :alt="이미지[index]" @click="modal(index)">
  <h4>{{ data[index].title }}</h4>
  <p>{{data[index].content}}</p>
  <p> {{ data[index].price }}</p>
  <button @click="신고수[index]++">허위매물신고버튼</button> <span> 신고수 : {{신고수[index]}}</span>

    </div>  -->



    <!-- <h4 :style="style">{{products[0]}}</h4>
    <p>{{price1}} 만원</p>
  </div>
  <div>
    <h4>{{products[1]}}</h4>
    <p>{{price2}} 만원</p>
  </div>
  <div>
    <h4>{{products[2]}}</h4>
    <p>{{price3}} 만원</p> -->



</template>

<script>

import data from './assets/data.js';
import Discount from './Discount.vue';
import Modal from './Modal.vue';
import Card from './Card.vue'

export default {
  name: 'App',
  data(){
    return{
      dataOriginal : [...data],
      누른거: 0,
      // UI법칙! UI의 상태를 data에 저장하고, data상태에 따라 어떻게 보일지 설정해주면 된다!
      모달창열렸니 : false, 
      메뉴들 : ['Home', 'Shop', 'About'],
      price : [60, 70, 80],
      style : 'color : blue',
      신고수 : [0,0,0,0,0,0],
      이미지 : [
        require('./assets/room0.jpg'),require('./assets/room1.jpg'),require('./assets/room2.jpg'),
      ],
      data,
      showDiscount : true,
      disCountPercent : 30,
    }
  },
  components: {
    // Discount : Discount,
    Discount : Discount,
    Modal : Modal,
    Card : Card,
    
  },
  
  methods: {
    increase(){
      this.신고수 += 1;
    },
    modal(index){
      this.모달창열렸니 = !this.모달창열렸니
      this.누른거 = index
    },
    priceSort(){
      this.data.sort((a,b) => a.price - b.price)
      console.log(this.data)
    },
    priceSortReverse(){
      this.data.sort((a,b) => b.price - a.price)
    },
    abcSort(){
      this.data.sort((a,b) => {
        let x = a.title.toLowerCase();
        let y = b.title.toLowerCase();
        if (x < y){
          return -1
        }
        else if (x > y) {
          return 1
        }
        else {
          return 0
        }
      })
    },
    resetSort(){
      this.data = [...this.dataOriginal];
      console.log(this.dataOriginal)
      console.log(this.data)
    },
    filterSort(){
      let highPrice = this.data.filter((datum) => datum.price > 500000)
      this.data = [...highPrice]
    }
  },

  mounted() {
    let timer = setInterval(()=>{
      this.disCountPercent--;
      if(this.disCountPercent <=0){
        clearInterval(timer)
      }
    }, 200);
  // 서버에서 데이터 가져올 때도 mounted 혹은 created라는 훅 둘 중에 한 곳에 걸어준다.
  },



}
</script>

<style>

.fade-leave-from{
opacity: 1
}
.fade-leave-active{
  transition: all 1s;
}
.fade-leave-to{
opacity: 0;
}

.fade-enter-from{
opacity: 0;
transform:translateY(-1000px);
}
.fade-enter-active{
  transition: all 1s;
}
.fade-enter-to{
opacity: 1;
transform:translateY(0px);

}



#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}

.menu{
background: darkslateblue;
padding: 15px;
border-radius: 5px;
}

.menu a {
color:white;
padding:10px;
}

img{
width:100%;
margin-top:40px;
}




body{
  margin:0
}

div{
  box-sizing: border-box;
}

.black-bg{
  width:100%;
  height: 100%;
  background: #0005;
  position: fixed;
  padding: 20px;
}

.white-bg{
  width:100%; background: white;
  border-radius: 8px;
  padding: 20px;
}



</style>
