<template>
  <!-- 메뉴 -->
  <div class="menu" >
    <a v-for="menu in menus" :key="menu">{{ menu }}</a>
  </div>

  <!-- 할인 안내-->
  <Discount v-if="showDiscnt === true"/>

  <button @click="priceSort">가격순정렬</button>
  <button @click="sortBack">초기화</button>

  <!-- 메인 -->
  <Card 
    :roomInfo="roomInfos[i]" 
    :count="count"
    v-for="(roomInfo, i) in roomInfos" 
    :key="roomInfo" 
    @clickTitle="openModal($event), $event"
    @increaseCnt="increaseCnt(), $event"
  />

  <!-- 상세 모달창 -->
  <transition name="fade">
  <Modal 
    :roomInfos="roomInfos" 
    :clickId="clickId" 
    :modalOpenYn="modalOpenYn"
    @closeModal="modalOpenYn=false" 
  />
  </transition>
  <!-- <div class="start" :class="{ end : modalOpenYn }">
    <Modal />
  </div> -->

</template>

<script> 
import roomInfo from './assets/data.js';
import Discount from './components/Discount.vue';
import Card from './components/Card.vue';
import Modal from './components/Modal.vue';

export default {
  name: 'App',
  data(){
    return {
      menus : ['Home','Shop','About'],
      roomInfos : roomInfo,
      roomsOrigin : [...roomInfo], //데이터 변형없게 하기 위해 원본의 사본 저장
      clickId : 0,
      modalOpenYn : false,
      count : 0,
      showDiscnt : false
    }
  },
  methods: {
    increaseCnt() {
      this.count += 1;
    },
    openModal(id){
      console.log(this.roomInfos[this.clickId])
      this.modalOpenYn = true; 
      this.clickId = id;
    },
    priceSort(){
      this.roomInfos.sort(function(a,b){
        return a.price - b.price ; // 양수,음수 결과에 따라 정렬함 (오름차순)
        // return b.price - a.price ; // 내림차순
      });
    },
    sortBack(){
      this.roomInfos = [...this.roomsOrigin];
    }
  },
  mounted(){
    setTimeout(() => {
      /**
       * ()=> arrow function 사용 장점
       * 바깥에 있는 this를 가져와서 함수 실행 가능
       * cf) function() -> this. ((X))
      */
      // ()=> arrow function 사용 장점
      // 바깥에 있는 this를 가져와서 함수 실행 가능
      // cf) function() -> X
      this.showDiscnt = true;
    }, 2000);
  },
  components: {
    Discount,
    Card,
    Modal
  }
}
</script>

<style>
body {
  margin : 0;
}
div {
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color:aliceblue;
  padding: 5px;
}
.title_style{
  color : green;
  cursor:pointer;
}
.room_img{
  width: 90%;
  margin-top: 30px;
}
.black-bg{
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed;
  padding:20px;
}
.white-bg{
  width: 100%;
  background: white;
  border-radius: 8px;
  padding:20px;
}

/** transition 기본 원리 */
.start {
  opacity: 0;
  transition: all 1s;
}
.end {
  opacity: 1;
}

/** OPEN transition 적용 "name"-___-_____ */
.fade-enter-from {
  opacity: 0;
  transform:translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
  transform:translateY(1000px);
}
/** CLOSE transition 적용 "name"-___-_____ */
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0leave
}

</style>
