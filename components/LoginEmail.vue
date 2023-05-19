<template>
  <el-form ref="loginForm" :model="loginForm" :rules="loginFormRules" label-width="80px">
    <el-form-item label="邮箱" prop="email">
      <!-- 使用 element 的 input 组件 -->
      <el-input v-model="loginForm.email"></el-input>
    </el-form-item>
    <el-form-item label="密码" prop="password">
      <!-- 使用 element 的 input 组件，type 属性设置为 password -->
      <el-input type="password" v-model="loginForm.password"></el-input>
    </el-form-item>
    <el-form-item>
      <!-- 使用 element 的 button 组件提交表单 -->
      <el-button type="primary" @click="login">登录</el-button>
    </el-form-item>
  </el-form>
</template>

<script lang="ts">
export default {
  data() {
    return {
      // 表单数据对象
      loginForm: {
        email: '',
        password: ''
      },
      // 表单数据校验规则
      loginFormRules: {
        email: [
          { required: true, message: '请输入邮箱', trigger: 'blur' }, // 输入框失去焦点时触发校验
          { type: 'email', message: '请输入有效的邮箱地址', trigger: ['blur', 'change'] }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 20, message: '密码长度应为 6 到 20 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    login() {
      // 使用 element 的 validate 方法进行表单校验
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          // 表单校验通过，执行登录逻辑
          console.log('登录成功')
        } else {
          // 表单校验不通过，提示错误信息
          console.log('校验不通过')
          return false
        }
      })
    }
  }
}
</script>
