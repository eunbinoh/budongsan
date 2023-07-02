<template>
  <div>
    <img src="../assets/room0.jpg" class="room_img">
    <!-- <img :src="roomInfo.image" class="room_img"> -->
    <h4 class="title_style" @click="$emit('clickTitle', roomInfo.id)"> {{ roomInfo.title }} </h4>
    <p> {{ roomInfo.price }} 만원 </p>
    <button @click="$emit('increaseCnt', count)">허위매물신고</button> <span>신고수: {{ count }}</span>
  </div>
</template>

<script>
export default {
    name: 'Card_a',
    props: {
        roomInfo : Object,
        count : Number
    },
    methods: {
        //function() {
        //     this.$emit('clickTitle', this.roomInfo.id)
        // }

    }
}
</script>

<style>

</style>