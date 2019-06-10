<template>
<div>
    <div class="header">备忘录</div>
    <el-form
      :model="ruleForm"
      status-icon
      :rules="rules"
      ref="ruleForm"
      label-width="100px"
      class="login"
    >
      <el-form-item label="用户名" prop="name">
        <el-input v-model.number="ruleForm.age"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="pass">
        <el-input type="password" v-model="ruleForm.pass" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item class="login_button">
        <el-button type="primary" @click="submitForm('ruleForm')">注册</el-button>
        <el-button @click="resetForm('ruleForm')">登录</el-button>
      </el-form-item>
    </el-form>
</div>
</template>

<script>
export default {
  name: 'Login',
  data() {
    var checkName = (rule, value, callback) => {
      if (value === '') {
        return callback(new Error('用户名不能为空'));
      }
    }
    var validatePass = (rule, value, callback) => {
      if (value === '') {
        callback(new Error('请输入密码'))
      } else {
        if (this.ruleForm.checkPass !== '') {
          this.$refs.ruleForm.validateField('checkPass')
        }
        callback()
      }
    }
    return {
      ruleForm: {
        pass: '',
        checkname: ''
      },
      rules: {
        pass: [{ validator: validatePass, trigger: 'blur' }],
        name: [{ validator: checkName, trigger: 'blur' }]
      }
    }
  },
  methods: {
    submitForm(checkName) {
      this.$refs[checkName].validate(valid => {
        if (valid) {
          this.$router.push('/home')
        } else {
          console.log('error submit!!')
          return false
        }
      })
    },
    resetForm(formName) {
      this.$refs[formName].resetFields()
      this.$refs[formName].validate(valid => {
        if (valid) {
          // 使用 vue-router 路由到指定页面，该方式称之为编程式导航
          this.$router.push('/home')
        } else {
          this.dialogVisible = true
          return false
        }
      })
    }
  }
}
</script>

<style lang="stylus" scoped>
.header {
  line-height: 150px;
  background: #409EFF;
  color: #fff;
  font-size: 20px;
  text-align: center;
}

.login {
  display: block;
  margin-top: 130px;
  margin-right: 40px;
}

.login_button {
  display: flex;
  margin-left: 40px;
}
</style>
