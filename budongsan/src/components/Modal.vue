<template>
    <div class="black-bg" v-if="modalOpenYn == true">
    <div class="white-bg">
      <img src="../assets/room0.jpg">
      <h4>{{ roomInfos[clickId].title }}</h4>
      <p>{{ roomInfos[clickId].content }}</p>
      
      <input type="text" v-model="month" >
      <!-- <input type="range" min="1" max="12" v-model="month" > -->
      <!-- <input   @input="month = $event.target.value" > -->
      <p>{{month}}개월 가격: {{ roomInfos[clickId].price * month }} 만원</p>

    </div>
    <button @click="$emit('closeModal')">Close</button>
  </div>
</template>

<script>
export default {
    name: 'Modal_a',
    data(){
        return {
            month : 1,
        }
    },
    watch : {
        //감시하고싶은 변수명으로 함수명
        month(n){
            if (n > 12){
                alert('12개월 이상 입력할 수 없습니다.');
                this.month = 12;
            } 
            if (isNaN(n)){
                alert('숫자만 입력하세요.')
                this.month = 1;
            }
        }
    },
    props: {
        roomInfos : Array,
        clickId: Number,
        modalOpenYn : Boolean
    },
    methods:{

    },
    // beforeUpdate(){
    //     if (this.month === 2){
    //         alert('2개월 할인은 선택할 수 없습니다.');
    //     } 
    // }
}
</script>

<style>

</style>