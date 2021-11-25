<template>
<div class="black-bg" v-if="모달창열렸니 === true">
  <div class="white-bg">
  <img :src="data[누른거].image" alt="">
  <h4>{{ data[누른거].title }} </h4>
  <p>{{ data[누른거].content}} </p>
  <p>{{ data[누른거].price}}원 / 개월</p>
  <!--<input @input="month = $event.target.value" placeholder="몇개월 할 거임">   요거의 축약 버전이 아래! -->
 <input v-model="month" placeholder="몇개월 할 거임">
 <input type="range" min="1" max="12" v-model = "month">
      <!--<br>
  <textarea v-model = "month"></textarea> -->
  <p> {{ month }} 개월 선택함 : {{data[누른거].price * month}}원</p>
  <!-- event = eventListener의 파라미터 e랑 비슷한 동작. -->
  <button @click="모달창닫기">닫기</button>
  </div>
</div>
</template>


<script>
    export default{
        name : 'Modal',
        props : {
            data : Object,
            누른거 : Number,
            모달창열렸니 : Boolean,
        },
        watch : {
            // a는 변경 될 month 데이터, b는 변경 전 데이터
            month(a){
                    if(isNaN(a) == true){
                        alert('숫자로 입력해주세요')
                        this.month = 1
                    }
                },
            },
        

        data(){
            return{
                // month : '0', 만약 텍스트를 받을 거면 초기값을 문자로 해 둘 것!
                month : '1',
            }
        },
        methods : {
            모달창닫기(){
                this.$emit('modalClose')
                this.month = 0
            }
        },

          beforeUpdate() {
    if (this.month == 2){
      alert('에이 2개월은 안팔아요 퉷')
    this.month = 3
    }
  }
    }
</script>

<style>

</style>