<!--
 * @FileDescription: 用户端登录
 * @Author: 郑仪登录、陈思羽注册
 * @Date: ——
 * @LastEditors: 李思佳
 * @EditDescription: 外联的css应该写在<style></style>标签里面嗷，<script></script>标签里是写js操作的。
 * @LastEditTime: ——
-->
<template>
  <div class="out">
    <div class="h11">
      <h1 class="title">信 息 分 享 中 心</h1>
    </div>
    <div class="radio1">
      <el-radio v-model="radio" label="1" @change="toggleContent" >登录</el-radio>
      <el-radio v-model="radio" label="2" @change="toggleContent">注册</el-radio>
    </div>
    <!-- 登录 -->
    <div class="wz" v-if="showLogin">
      <el-input class="rounded-input" style="margin-bottom: 15%;" v-model="email"  placeholder="请输入邮箱" ></el-input>
      <el-input class="rounded-input" v-model="password" style="margin-bottom: 20%;" placeholder="请输入密码" ></el-input>
      <button class="rounded-button" type="primary" plain @click="getPostData">登录</button>
      <p v-if="loginError" class="error-message">{{ loginErrorMessage }}</p>
    </div>
    <!-- 注册 -->
    <div class="wz" v-else>
      <el-input class="rounded-input" v-model="input" placeholder="请输入邮箱">
      </el-input>
      <el-input class="rounded-input" v-model="input" placeholder="请输入姓名">
      </el-input>
      <el-input class="rounded-input" v-model="input" placeholder="请输入专业班级">
      </el-input>
      <el-select class="selectStyle" v-model="value" placeholder="请选择">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
  <el-input class="rounded-input" v-model="input" placeholder="请输入密码">
      </el-input>
      <el-input class="rounded-input" v-model="input" placeholder="请输入验证码">
      </el-input>
      <button class="rounded-button" type="primary" plain @click="login">注册</button>
      </div>
    <div class="tuu">
      <img src="../assets/images/copy-right.png">
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginError: false, // 是否显示错误提示
      loginErrorMessage: '', // 登录错误提示消息
      options: [{
        value: '前端',
        label: '前端'
      }, {
        value: '后端',
        label: '后端'
      }, {
        value: '设计',
        label: '设计'
      }, {
        value: '人工智能',
        label: '人工智能'
      }],
      value: '',
      radio: '1',
      input: '',
      showLogin: true,
      password: '',
      email: ''
    }
  },
  methods: {
    async getPostData () {
      const { data: res } = await this.$axios.post('http://150.158.53.178:6290/api/login', {
        email: this.email,
        password: this.password
      })
      console.log(res)
    },
    async login () {
      // 添加验证逻辑
      if (this.email === '' || this.password === '') {
        this.loginError = true
        this.loginErrorMessage = '邮箱和密码不能为空'
      }
    },
    // 发送登录请求
    toggleContent () {
      // 点击注册按钮时切换显示的内容
      this.showLogin = !this.showLogin
    }
    // signin () {
    //   this.$router.push('/SignIn')
    // }
  }
}
</script>

<style scoped>
@import '../assets/css/loginIn.css';
.el-radio__label {
  color: #fff;
}

</style>
