<template>
  <div class="login-wrap">
    <el-form label-position="top" label-width="80px" :model="formdata" class="login-form">
      <h2 class="login-title">后台管理系统</h2>
      <el-form-item label="用户名">
        <el-input v-model="formdata.username" placeholder="请输入用户名"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="formdata.password" placeholder="请输入密码" show-password></el-input>
      </el-form-item>
      <el-button type="primary" @click.prevent = "handleLogin()" class="login-btn">登录</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  data () {
    return {
      formdata: {
        username: '',
        password: ''
      }
    }
  },
  methods: {
    handleLogin () {
      this.$http.post('/login', this.formdata).then(res => {
        console.log(res)
      })
    }
  }
}
</script>

<style>
.login-wrap{
    height: 100%;
    background-color: #324152;
    display: flex;
    justify-content: center;
    align-items: center;
}
.login-wrap .login-form {
    width: 350px;
    background-color: #fff;
    border-radius: 5px;
    padding: 30px;
}
.login-wrap .login-btn {
    width: 100%;
}
.login-wrap .login-title {
  text-align: center;
}
</style>
