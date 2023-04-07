<template>
  <h1>NH voucher 암호화</h1>
  <p><a href="https://documenter.getpostman.com/view/26725844/2s93RWQrLP#intro">NH Voucher API 명세서</a></p>
  
  <form v-on:submit.prevent="submitForm">
    <div>
      <label for="username">올원뱅크 암호화 전</label>
      <input id="username" type="text" v-model="preEncrpt">
    </div>
    <div>
      <label for="username">올원뱅크 암호화 후</label>
      <input v-bind:type="textarea" :value="encrypt">
    </div>

    <button type="submit">제출</button>
    <div>{{ encrypt }}</div>
    
  </form>
</template>

<script>
import axios from 'axios';

export default {
  data ()  {
    return {encrypt : ["초기값"]}
  },
    
  methods: { 
    submitForm: function() {
      var vm = this; //eslint-disable-line no-unused-vars
      // event.preventDefault();
      console.log(this.encrypt);
      this.encrypt = "변경값";
      console.log(this.encrypt);

      console.log(this.preEncrypt);

      const url = 'http://localhost:29347/aes256/gcm/encrypt';
      const data = {
        data: this.preEncrpt,
      }

      axios.post(url, data)
        .then(function(response) {  
          console.log("axios 통신 성공!");
          console.log(response);
          console.log(response.data);
          vm.encrypt = response.data;
          
          console.log(response.data);
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  }
}
</script>
<style>

</style>