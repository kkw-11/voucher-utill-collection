<template>
  <h1>NH voucher Util 모음</h1>
  <p><a href="https://documenter.getpostman.com/view/26725844/2s93RWQrLP#intro">NH Voucher API 명세서</a></p>
  
  <form v-on:submit.prevent="submitForm">
    <div>
      <label for="username">올원뱅크 암호화 전</label>
      <input id="username" type="text" v-model="username">
    </div>
    <div>
      <label for="password">pw: </label>
      <input id="password" type="password" v-model="password">
    </div>
    <button type="submit">제출</button>
  </form>
</template>

<script>
import axios from 'axios';

export default {
  data: function() {
    return {
      username: '',
      password: '',
    }
  },
  methods: {
    submitForm: function() {
      // event.preventDefault();
      console.log(this.username);
      const url = 'https://localhost:29347/aes256/gcm/encrypt';
      const data = {
        username: this.username,
      }
      axios.post(url, data)
        .then(function(response) {
          console.log(response);
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