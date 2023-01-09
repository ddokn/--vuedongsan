<template>
    <div class="black-bg" v-if="modal == true">
    <div class="white-bg">
      <h4>{{ onerooms[selectProduct].title }}</h4>
      <div>
        <img :src="onerooms[selectProduct].image">
        <p>
          {{ onerooms[selectProduct].content }}
        </p>
        <input type="text" v-model="month" maxlength="2">

        <p>{{ month }}개월 선택함: {{ onerooms[selectProduct].price * month }}원</p>
      </div>
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>

export default {
    name: 'productModal',
    data() {
      return {
        month: 1,
      }
    },
    watch: {
      month(a) {
        if ( a >= 13 ) {
          alert('13이상 입력하지 마셈');
        }
        if ( isNaN(a) == true ) {
          alert('글자 입력하지 마셈');
          this.month = 1;
        }
      }
    },
    props: {
        onerooms: Array,
        selectProduct: Number,
        modal: Boolean,
    }
}
</script>

<style>

</style>