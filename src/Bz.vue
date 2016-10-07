<template>
  <div class="ui segment">
    <div class="center aligned column">
      <form class="ui form fluid ">
        <div :class="{ 'error': user_name_error }" class="field">
          <label>用户名</label>
          <input @focus="cleanError" v-model="user_name" placeholder="请输入邮箱/用户名" type="text">
        </div>
        <div :class="{ 'error': password_error }" class="field">
          <label>密码</label>
          <input v-model="password" @keyup.enter="check" @focus="cleanError" placeholder="请输入密码"  type="password">
        </div>
        <a @click="check" :class="{ loading: loading }" class="ui blue submit button">登录</a>
      </form>
    </div>
  </div>
</template>

<script>
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
        loading: false,
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
        this.loading = true
        let parm = {}
        parm.user_name = this.user_name
        parm.password = this.password
        let _this = this

        window.fetch('/api_login', {
          credentials: 'same-origin',
          method: 'post',
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          body: JSON.stringify(parm)
        }).then(function (response) {
          _this.loading = false
          return response
        }).then(function (response) {
          return response.json()
        }).then(function (data) {
          if (data.error !== '0') {
            throw new Error(data.error)
          }
          _this.$emit('login_done')
        }).catch(function (error) {
          throw new Error(error)
        })
      }
    }
  }
</script>
<style>
</style>
