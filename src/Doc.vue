<style lang=less>
  .original-text-bz {
    /*保留空格*/
    white-space: pre-wrap;
    /*字体能自动换行*/
    word-wrap:break-word;
  }
  code {
    padding: 2px 4px;
    font-size: 90%;
    color: #c7254e;
    background-color: #f9f2f4;
    border-radius: 4px;
    .original-text-bz;
  }
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
  import 'bz-semantic-ui-card'
  import 'bz-semantic-ui-grid'
  import toastr from 'toastr'
  import Bz from './Bz'
  import Doc from 'bz-doc'
  export default {
    components: {
      Bz,
      Doc
    },
    route: {
      deactivate: function (transition) {
        this.$broadcast('unbind-scroll')
        transition.next()
      }
    },
    data: function () {
      return {
        name: 'bz-login',
        parms: [
          {parm: 'login', desc: '登录事件的句柄'},
          {parm: 'call_back', desc: '登录成功后的回调函数'}
        ],
        desc: '登录页面',
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

