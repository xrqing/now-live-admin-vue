<template>
  <div class="login-wrap">
    <el-form  ref="LoginFormRef" :rules="loginFormRules" label-position="top" label-width="80px" :model="formdata" class="login-form">
      <h2 class="login-title">体育后台管理系统</h2>
      <el-form-item label="用户名">
        <el-input v-model="formdata.username" placeholder="请输入用户名" ></el-input>
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
      },
      // 表单验证规则
      loginFormRules: {
        username: [
          { required: true, message: '请输入登录名', trigger: 'blur' },
          {
            min: 3,
            max: 10,
            message: '登录名长度在 3 到 10 个字符',
            trigger: 'blur'
          }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          {
            min: 6,
            max: 15,
            message: '密码长度在 6 到 15 个字符',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    handleLogin () {
      // 点击登录的时候先调用validate方法验证表单内容是否有误
      this.$refs.LoginFormRef.validate(async valid => {
        console.log(this.loginFormRules)
        // 如果valid参数为true则验证通过
        if (!valid) {
          return
        }
        // 发送请求进行登录
        const { data: res } = await this.$http.post('/login', this.formdata)
        //   console.log(res);
        if (res.code !== 200) {
          return this.$message.error('登录失败:' + res.message) // console.log("登录失败:"+res.meta.msg)
        }
        this.$message.success('登录成功')
        console.log(res)
        // 保存token
        window.sessionStorage.setItem('token', res.data.token)
        // 导航至/home
        this.$router.push('/home')
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
