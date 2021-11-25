<template>
  <div> 


 <img :src="datum.image">
  <h4 @click="모달창열기">{{ datum.title }}</h4>
  <p>{{datum.content}}</p>
  <p> {{ datum.price }}</p>
  <!-- <button @click="신고수[index]++">허위매물신고버튼</button> <span> 신고수 : {{신고수[index]}}</span> -->


</div>

</template>

<script>
export default { 
    props: {
        datum : Object,
    },
    methods : {
      모달창열기(){
        this.$emit('openModal',this.datum.id)
      }
    }
}

</script>


<style>

</style>