<template>
    <div class="discount" v-if="discountToggle || discountPercentage != 0">
        <h4>지금 결제하면 {{discountPercentage}}% 할인</h4>
    </div>
</template>

<script>
export default {
  name: 'DiscountBanner',
  data(){
    return {
        discountToggle: false,
        discountPercentage: 10,
    }
  },
  mounted(){
    // setTimeout(() => {
    //   this.discountToggle = false;
    // }, 2000)
    setInterval(() => {
      if (this.discountPercentage > 0) {
        this.discountPercentage--;
        }
    }, 1000)
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
