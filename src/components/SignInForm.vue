<template>
  <div>
    <form @submit.prevent="signIn">
      <div class="row">
        <label>用户名</label>
        <input type="text" required v-model="formData.username">
      </div>
      <div class="row">
        <label>密码</label>
        <input type="password" required v-model="formData.password">
      </div>
      <div class="actions">
        <input type="submit" value="提交">
        <span>{{errorMessage}}</span>
      </div>
    </form>
  </div>

</template>

<script>

import AV from '../lib/leancloud'
import getErrorMessage from '../lib/getErrorMessage'
import getAVUser from '../lib/getAVUser'

export default {
  name: 'SignInForm',
  data(){
    return {
      formData: {
        username: '',
        password: ''
      },
      errorMessage: ''
    }
  },
  methods: {
    signIn(){
      let {username, password} = this.formData
      AV.User.logIn(username, password).then(()=>{
        this.$emit('success', getAVUser())
      },(error)=>{
        this.errorMessage = getErrorMessage(error)
      })
    }
  }
}



</script>

<style lang="scss" >
.row {
  display: flex;
  justify-content: space-between;
  >input {
    margin-bottom: 20px;
    height: 30px;
    background-color: rgba(0,0,0,0.2);
  }
  >label {
    line-height: 30px;
  }
}
.actions {
  >input {
    display: block;
    width: 60px;
    height: 25px;
    background-color: rgba(0,0,0,0.4);
    color: white;
    border-radius: 3px;
    border: none;
    margin: 0 auto;
    cursor: pointer;

  }
}
</style>
