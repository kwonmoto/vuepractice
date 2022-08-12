<!-- eslint-disable vue/valid-v-on -->
<template>

  <!-- <div class="start" :class="{ end: modalToggle }"> -->
  <transition name="fade">
    <DetailModal 
      @closeModal="modalShow(false)" 
      :oneroom="oneroom" 
      :oneroomNum="oneroomNum" 
      :modalToggle="modalToggle" 
    />
  </transition>


  <div class="menu">
    <a v-for="i in menus" :key="i">{{ i }}</a>
  </div>

  <DiscountBanner />
  
  <button @click="sortPrice('asc')">가격 오름차순 정렬</button>
  <button @click="sortPrice('desc')">가격 내림차순 정렬</button>
  <button @click="sortPrice('clear')">초기화</button>

  <DetailCard @openModal="modalShow(true); nowNum($event)" v-for="(row) in oneroom" :key="row.id" :row="row"/>

</template>

<script>

import oneroom from './oneroom';
import DetailModal from './components/DetailModal.vue';
import DetailCard from './components/DetailCard.vue';
import DiscountBanner from './components/DiscountBanner.vue';

export default {
  name: 'App',
  data(){
    return {
      modalToggle: false,
      menus: ['Home', 'Shop', 'About'],
      originalOneroom: [...oneroom],
      oneroom: oneroom,
      colorstyle: 'color: darkslateblue',
      oneroomNum: 0
    }
  },
  methods: {
    modalShow(state) {
      this.modalToggle = state;
    },
    nowNum(i) {
      this.oneroomNum = i;
    },
    sortPrice(type) {
      if (type === "asc") {
        this.oneroom = this.oneroom.sort((a, b) => a.price - b.price);
      } else if (type === "desc") {
        this.oneroom = this.oneroom.sort((a, b) => b.price - a.price)
      } else this.oneroom = [...this.originalOneroom];
    }
  },
  components: {
    DetailModal,
    DetailCard,
    DiscountBanner
}
}
</script>

<style>

body {
  margin : 0
}

div {
  box-sizing: border-box;
}

.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}

.white-bg {
  width: 100%; background: white;
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

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
  cursor: pointer;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}

.product {
  margin-bottom: 10px;
}

.discount {
  background: #eee;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}

button {
  background: darkslateblue;
  color: white;
  border: none;
  border-radius: 10px;
  padding: 10px;
  cursor: pointer;
}

.start {
  opacity: 0;
  transition: all 0.5s;
}
.end {
  opacity: 1;
}

.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.5s;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 0.5s;
}
.fade-leave-to {
  opacity: 0;
}
</style>
