<template>
  <el-container>
    <el-header>{{tip}}</el-header>
    <el-main>
    <el-form ref="registform" :model="regist" label-width="60px">
      <el-form-item label="用户名">
        <el-input v-model="regist.username"></el-input>
      </el-form-item>
      <el-form-item label="手机号">
        <el-input v-model="regist.phonenumber"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="regist.password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="register">注册</el-button>
        <el-button @click="toLogin">返回</el-button>
      </el-form-item>
    </el-form>
    </el-main>
  </el-container>

</template>

<script>
export default {
  name: 'Register',
  data () {
    return {
      regist: {
        username: '',
        password: '',
        phonenumber: ''
      },
      tip: '5',
      loading: false
    }
  },
  methods: {
    register () {
      if(this.regist.username==''|this.regist.password==''||this.regist.phonenumber==''){
        this.tip = '内容不能为空，请重新输入'
      }else{
        this.$axios.post('user/register',{
          username: this.regist.username,
          password: this.regist.password,
          phone: this.regist.phonenumber
        }).then(response=>{
          if(response.data.code==200){
            this.loading=true;
            setTimeout(() => {
              loading.close();
            }, 1500);
            this.$router.replace({path:'/'})
          }else if(response.data.code!=0) {
            this.tip=response.data.msg;
          }
        })
      }
    },
    toLogin () {
      this.$router.replace({path: '/login'})
    }
  }
}
</script>

<style scoped>
.el-form{
  border-radius: 15px;
  background-clip: padding-box;
  margin: 90px auto;
  width: 350px;
  padding: 35px 70px 15px 35px;
  background: #fff;
  border: 1px solid #eaeaea;
  box-shadow: 0 0 25px #cac6c6;
}
</style>
