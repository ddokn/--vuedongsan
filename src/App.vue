<template>


  <transition name="fade">
    <Modal @closeModal="modal = false" :onerooms="onerooms" :selectProduct="selectProduct" :modal="modal"/>
  </transition>

  <Menu :menu="menu"/>
  
  <Discount v-if="showDiscount  == true" />


  <button @click="priceSort">가격순정렬</button>
  <button @click="priceRevertSort">가격역순정렬</button>
  <button @click="priceStringSort">가나다정렬</button>


  <button @click="sortBack">되돌리기</button>


  <Card @openModal="modal = true; selectProduct = i" :oneroom="onerooms[i]" v-for="(b, i) in 6" :key="i"/>
  
</template>

<script>

import data from './assets/oneroom.js';
import Discount from './components/Discount.vue';
import Modal from './components/Modal.vue';
import Card from './components/Card.vue';
import Menu from './components/Menu.vue';

export default {
  name: 'App',
  data() {
    return {
      showDiscount: true,
      selectProduct: 0,
      oneroomOriginal: [...data], // 각각 별개의 사본을 만들 때
      onerooms: data,
      modal: false,
      count: [0, 0, 0],
      menu: ['Home', 'Shop', 'About'],
      products: [],
    }
  },
  methods: {
    increase(){
      this.count += 1;
    },
    priceSort(){
      this.onerooms.sort(function(a,b){ // sort 원본 데이터가 변형됨
        return a.price - b.price
      });
    },
    priceRevertSort() {
      this.onerooms.sort(function(a,b){
        return b.price - a.price
      });
    },
    priceStringSort() {
      this.onerooms.sort(function(a,b){
        if ( a.title < b.title ) return -1; 
        else if ( a.title == b.title ) return 0; 
        else return 1; 
      });
    },
    sortBack(){
      this.onerooms = [...this.oneroomOriginal];
    }
  },
  mounted(){
    // setTimeout(()=>{
    //   this.showDiscount = false
    // }, 2000);
    setInterval(()=>{
      
    }, 1000);
  },
  components: {
    Discount,
    Modal,
    Card,
    Menu,
  }
}
</script>

<style>
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
  color: #fff;
  padding: 10px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
.black-bg {
  width: 100%;
  height: 100%;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  padding: 20px;
}
.white-bg {
  width: 100%;
  background: #fff;
  border-radius: 8px;
  padding: 20px;
}
.white-bg img {
  width: 100%;
}
.discount {
  background: #EEE;
  padding: 10px;
  margin: 10px;
  border-radius: 5px;
}
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  opacity: 1;
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

</style>
