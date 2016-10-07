<template>
  <div>
    <doc :name="name"
    :desc="desc"
    :parm_desc="parm_desc"
    :parms="parms"
    :code="code"
    >
    <bz v-on:login_done="call_back"></bz>
    </doc>
  </div>
</template>
<script>
  import toastr from 'toastr'
  import 'toastr/build/toastr.min.css'
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
        name: 'bz-login',
        desc: '登录页面',
        parms: [
          {parm: 'login_done', desc: 'v-on 绑定 login_done事件，回调login成功后的操作'}
        ],
        parm_desc: ``,
        code: `<bz v-on:login_done="call_back"></bz>`
      }
    },
    methods: {
      call_back: function () {
        toastr.info('登录成功')
      }
    }
  }
</script>
<style>
</style>
