<template>
  <div class="login">
    <p style="text-align: center">登陆</p>
    <el-form ref="loginFormRef" :model="loginForm" status-icon :rules="loginFormRules" label-width="100px" class="demo-ruleForm" label-position="left">

      <el-form-item label="用户名：" prop="name">
        <el-input v-model="loginForm.name" type="text" autocomplete="off" />
      </el-form-item>

      <el-form-item label="密码：" prop="password">
        <el-input v-model="loginForm.password" type="password" autocomplete="off" show-password @keyup.enter.native="submitForm" />
      </el-form-item>

      <el-form-item>
        <el-button type="primary" @click="submitForm">登录</el-button>
        <el-button @click="resetForm">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    var sPhonenumber = (rule, value, callback) => {
      // eslint-disable-next-line eqeqeq
      if (value == '') {
        callback(new Error('请输入账号'))
      } else {
        callback()
      }
    }
    var sPass = (rule, value, callback) => {
      // eslint-disable-next-line eqeqeq
      if (value == '') {
        callback(new Error('请输入密码'))
      } else {
        callback()
      }
    }
    return {
      loginForm: {
        sPhonenumber: '',
        sPass: ''
      },
      loginFormRules: {
        sPhonenumber: [
          { validator: sPhonenumber, trigger: 'blur' }
        ],
        sPass: [
          { validator: sPass, trigger: 'blur' }
        ]
      },
      redirect: undefined,
      otherQuery: {},
      loading: false
    }
  },
  watch: {
    $route: {
      handler: function(route) {
        const query = route.query
        if (query) {
          this.redirect = query.redirect
          this.otherQuery = this.getOtherQuery(query)
        }
      },
      immediate: true
    }
  },
  created() {
    window.sessionStorage.removeItem('token')
  },
  methods: {
    // 登录查询，或者说是按下登录键之后查询
    submitForm() {
      // eslint-disable-next-line no-unused-vars
      this.$refs.loginFormRef.validate((valid) => {
        this.$axios.post('login', this.loginForm).then(res => {
          console.log(typeof (res.data))
          if (typeof (res.data) === 'string') {
            this.$message.error(res.data)
          } else {
            window.sessionStorage.setItem('token', JSON.stringify(res.data))
            this.$router.push({ path: this.redirect || '/', query: this.otherQuery })
            this.loading = false
          }
          console.log(res)
        }).catch(() => {
          this.loading = false
        })
      })
    },
    getOtherQuery(query) {
      return Object.keys(query).reduce((acc, cur) => {
        if (cur !== 'redirect') {
          acc[cur] = query[cur]
        }
        return acc
      }, {})
    },
    // 重置按钮
    resetForm() {
      console.log(this)
      this.$refs.loginFormRef.resetFields()
    }
  }
}
</script>

<style scoped>
  .login{
    width: 400px;
    margin: auto;
    padding: 20px;
    margin-top: 60px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
  }
</style>
