<template>
  <h1>NH voucher 암복호화 테스트</h1>
  <p><a href="https://documenter.getpostman.com/view/26725844/2s93RWQrLP#intro">NH Voucher API 명세서</a></p>
  
  <form v-on:submit.prevent="submitForm">
    <div>
      <label>올원뱅크 암호화 전</label>
      <input id="username" type="text" v-model="preEncrypt">
    </div>
    <div>
      <label> 올원뱅크 암호화 후</label>
      <input type="textarea" :value="encrypt">
    </div>

    <button type="submit">제출</button>
    <div>{{ encrypt }}</div>
    
  </form>
</template>
<script setup>
import axios from 'axios';
import { ref } from 'vue';

const encrypt = ref("초기값");
const preEncrypt = ref('');

const submitForm = () => {
  console.log(encrypt);
  encrypt.value = "변경값";
  console.log(encrypt);
  console.log(preEncrypt);

  const url = 'http://localhost:29347/aes256/gcm/encrypt';
  const data = {
    data: preEncrypt.value
  }

  axios.post(url, data)
    .then(function(response) {  
      console.log("axios 통신 성공!");
      console.log(response);
      console.log(response.data);
      encrypt.value = response.data;
      console.log(response.data);
    })
    .catch(function(error) {
      console.log(error);
    });
}
</script>
<style>

</style>