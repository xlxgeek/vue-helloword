<template>
  <div>
    <blog-header></blog-header>
    <hr/>
    <div>
      用户名:<input type="text" v-model="loginInfoVo.username" placeholder="请输入用户名" />
      <br/>
      密码：<input type="password" v-model="loginInfoVo.password" placeholder="请输入密码" />
      <br/>
      <button v-on:click="login">登录</button>
      <br/>
      登录验证情况：<textarea cols="30" rows="10" v-model="responseResult"></textarea>
    </div>
    <hr/>
    <blog-footer></blog-footer>
  </div>
</template>
<script>
import blogHeader from '@/components/common/BlogHeader.vue'
import blogFooter from '@/components/common/BlogFooter.vue'

export default {
  name: 'BlogLogin',
  // blogHeader、blogFooter组件给申明到components里面然后在template里面使用
  components: { blogHeader, blogFooter },
  data () {
    return {
      loginInfoVo: { username: '', password: '' },
      responseResult: []
    }
  },
  methods: {
    login () {
      console.log(this.loginInfoVo.username)
      this.$axios({
        method: 'post',
        url: '/hydro/login/login/',
        headers: {
          'Content-Type': 'application/json;charset=UTF-8'
        },
        // data: { username: this.loginInfoVo.username,
        //   password: this.loginInfoVo.password}
        params: {username: this.loginInfoVo.username,
          password: this.loginInfoVo.password }
      }).then(data => {
        console.log(data)
      }).catch(failResponse => {})
    }
  }
}
</script>
