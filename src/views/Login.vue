<template>
  <div class="login">
    <el-form ref="form" :rules="rules" :model="form" label-width="80px" class="login-box">
      <h3 class="login-title">欢迎登录</h3>
      <el-form-item label="用户名" prop="name">
        <el-input v-model="form.name"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input type="password" v-model="form.password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="onSubmit('form')">登录</el-button>
        <el-button @click="onRegister">注册</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

import axios from "axios";

export default {
  name: 'Login',
  data () {
    return {
      form: {
        name: '',
        password: ''
      },
      rules: {
        name: [
          {
            required: true,
            message: '请输入用户名',
            trigger: 'blur'
          },
          {
            min: 3,
            max: 50,
            message: '长度在 3 到 50 个字符',
            trigger: 'blur'
          }
        ],
        password: [
          {
            required: true,
            message: '密码不能为空',
            trigger: 'blur'
          },
          {
            min: 6,
            max: 50,
            message: '长度在 6 个字符以上',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    onSubmit (formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          // window.sessionStorage.setItem('isLogin', 'true')
          // this.$store.dispatch('asyncUpdateUser', { name: this.form.name })
          // 页面跳转
          // this.$router.push('/Main')
          // this.$router.push({
          //   name: 'Main',
          //   params: { name: this.form.name }
          // })

          axios.post('', {
            name: '',
            password: ''
          })
              .then(function (res) {
                console.log(res);
              })
              .catch(function (err) {
                console.log(err);
              });

          axios.get('https://autumnfish.cn/api/joke/list?num=4')
              .then(function (response) {
                console.log(response.data.jokes[0])
              }).catch(function (error) {
                console.log(error);
              });
          this.$router.push({ name: 'Main' , replace: true})
        } else {
          alert('error submit!!')
          return false
        }
      })
    },
    onRegister (re) {
      this.$router.replace('/Register')
    }
  }
}

</script>

<style>
.login-box {
  width: 400px;
  margin: 200px auto;
  border: 1px solid #DCDFE6;
  padding: 40px;
  border-radius: 10px;
  box-shadow: 0 0 30px #DCDFE6;
}

.login-title {
  text-align: center;
}

</style>
