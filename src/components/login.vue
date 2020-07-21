<template>
  <el-container style="height: 500px">
      <el-header></el-header>
        <el-container style="background-color: lightcyan;">
          <el-aside width="60%"></el-aside>
          <el-form ref="loginform" :model="loginform" label-width="60px" style="width: 300px;">
            <el-form-item label="手机号">
              <el-input v-model="loginform.phonenumber"></el-input>
            </el-form-item>
            <el-form-item label="密码">
              <el-input v-model="loginform.password"></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="login">登陆</el-button>
              <el-button @click="toRegist()">注册</el-button>
            </el-form-item>
          </el-form>
        </el-container>
  </el-container>
</template>

<script>
export default {
  name: "login",
  data () {
    return{
      loginform: {
        phonenumber: '',
        password: ''
      }
    }

  },
  methods: {
    login () {
      this.$axios.post('/login', {
        phonenumber: this.loginform.phonenumber,
        password: this.loginform.password
      }).then(response => {
        console.log(response)
        console.log(response.data.message)
        if(response.data.msg=="succeed"){
          console.log(response.data.code)
          this.$router.replace({path:'/'})
        }
      })

    },
    toRegist () {
      this.$router.replace({path:'/register'})
    }
  }
}
</script>

<style scoped>
    .el-main {
      /*background-image: url("../assets/bg.jpg");*/
      background-color: lightcyan;

    }
  .el-form{
    margin-top: 100px;
    margin-bottom: 180px;
    padding-top: 50px;
    padding-bottom: 50px;
    padding-right: 50px;
    background-color: aliceblue;
  }
</style>
