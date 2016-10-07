<template>
  <div class="ui segment">
    <div class="center aligned column">
      <form class="ui form fluid ">
        <div v-bind:class="{ 'error': user_name_error }" class="field">
          <label>用户名</label>
          <input @focus="cleanError" v-model="user_name" placeholder="请输入邮箱/用户名" type="text">
        </div>
        <div v-bind:class="{ 'error': password_error }" class="field">
          <label>密码</label>
          <input v-model="password" @keyup.enter="check" @focus="cleanError" placeholder="请输入密码"  type="password">
        </div>
        <a @click="check" class="ui blue submit button">登录</a>
      </form>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue'
  import VueResource from 'vue-resource'
  Vue.use(VueResource)
  var api_login = Vue.resource('/api_login{/parm}')
  import toastr from 'toastr'
  import 'bz-semantic-ui-form'
  import 'bz-semantic-ui-button'
  export default {
    props: {
    },
    components: {
    },
    data: function () {
      return {
        user_name: '',
        user_name_error: false,
        password: '',
        password_error: false
      }
    },
    ready () {
    },
    methods: {
      check: function () {
        if (!this.user_name) {
          this.user_name_error = true
          toastr.error('请输入用户名')
          return
        }
        if (!this.password) {
          this.password_error = true
          toastr.error('请输入密码')
          return
        }
        this.login()
      },
      cleanError: function () {
        this.user_name_error = false
        this.password_error = false
      },
      login: function () {
        let parm = {}
        parm.user_name = this.user_name
        parm.password = this.password

        api_login.save(parm).then(
          (response) => {
            if (response.data.error !== '0') {
              throw new Error(response.data.error)
            }
            this.$emit('login_done')
          },
          (response) => {
          }
        )
      }
    }
  }
</script>
<style>
</style>
