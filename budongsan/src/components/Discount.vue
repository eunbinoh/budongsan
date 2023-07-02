<template>
  <div class="discount">
    <h4>지금 결제하면 {{discountRat}} % 할인</h4>
  </div>
</template>

<script>
export default {
    name : 'Discount_a',
    data(){
        return {
            discountRat : 30
        }
    }
}
</script>

<style>
.discount {
  background: #eee;
  padding: 10px;
  margin:10px;
  border-radius: 5px;
}
</style>