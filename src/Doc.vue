<style>
</style>
<template>
  <div>
    <doc :name="name"
    :desc="desc"
    :parm_desc="parm_desc"
    :parms="parms"
    :code="code"
    >
    <bz :login="login" :call_back="call_back"></bz>
    </doc>
  </div>
</template>
<script>
  import toastr from 'toastr'
  import 'bz-semantic-ui-card'
  import 'bz-semantic-ui-grid'
  import Bz from './Bz'
  import Doc from 'bz-doc'
  export default {
    components: {
      Bz,
      Doc
    },
    data: function () {
      return {
        datas: [1],
        name: 'bz-login',
        desc: '登录页面',
        parms: [
          {parm: 'login', desc: '登录验证等操作函数'},
          {parm: 'call_back', desc: '登录成功后的回调函数'}
        ],
        parm_desc: `注意，如果使用的组件有路由，那么最好在切换路由的时候发送消息，解除绑定(参看本例子) <code>this.$broadcast('unbind-scroll')</code>`,
        code: `<login :login="login" :call_back="call_back"></login>`
      }
    },
    methods: {
      call_back: function () {
        toastr.info('登录成功')
      },
      login: function (params) {
        console.log(params)
        window.alert('干登录的事')
      }
    }
  }
</script>
