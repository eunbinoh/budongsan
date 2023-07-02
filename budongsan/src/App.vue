<template>

  <!-- 할인 안내-->
  <Discount />
  
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

  <!-- 메뉴 -->
  <div class="menu" >
    <a v-for="menu in menus" :key="menu">{{ menu }}</a>
  </div>

  <!-- 메인 -->
  <Card 
    :roomInfo="roomInfos[i]" 
    :count="count"
    v-for="(roomInfo, i) in roomInfos" 
    :key="roomInfo" 
    @clickTitle="openModal($event), $event"
    @increaseCnt="increaseCnt($event), $event"
  />


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
      clickId : 0,
      modalOpenYn : false,
      count : 0
    }
  },
  methods: {
    increaseCnt(count) {
      this.count = count++;
    },
    openModal(id){
      this.modalOpenYn = true; 
      this.clickId = id;
    }
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
