<template>
  <div class="loginPopup" v-if="loginPopup">
    <div class="loginContent">
      <h3>Login with</h3>
      <div class="metaMaskImage">
        <a class="metaMaskLogin" v-on:click="loginWithMetaMask"></a>
      </div>
      <b-form-input v-model="userID" type="text" placeholder="ID" :disabled="isLoggedIn"></b-form-input>
      <b-button variant="primary" v-on:click="setUserID_req(userID)" id="setUserID" v-if="!isLoggedIn">Set User ID</b-button>
    </div>
  </div>
</template>

<script>
  import helper from '../utils/helper';

  export default {
    name: 'login',
    props: [
     'isLoggedIn',
     'loginPopup'
    ],
    data() {
      return {
        userID: ''
      };
    },
    methods: {
      async loginWithMetaMask() {
        const userId = await window.web3.eth.getCoinbase();
        this.setUserID_req(window.web3.utils.toChecksumAddress(userId));
      },
      setUserID_req(userId) {
        helper.data.bus.$emit('doLogin', userId);
      }
    }
  };

</script>
