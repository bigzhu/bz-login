<template>
  <div class="ui segment">
    <div>
      <h1>Login</h1>
      <p>
        登录
      </p>
      <table class="ui celled table">
        <thead>
          <tr><th>参数</th><th>说明</th></tr>
        </thead>
        <tbody>
          <tr v-for="parm in parms"> <td class="single line"> {{parm.parm}} </td> <td> {{parm.desc}} </td></tr>
          <tr v-show="parms.length===0">
            <td colspan="2">这货没有参数</td>
          </tr>
        </tbody>
      </table>
    </div>
    <code v-text="code">
    </code>
    <div class="ui divider"></div>
    <login :login="login" :call_back="call_back"></login>
  </div>
</template>
<script>
  import Login from './Bz'
  import toastr from 'toastr'
  export default {
    components: {
      Login
    },
    data: function () {
      return {
        parms: [
          {parm: 'call_back', desc: '登录成功后的回调函数'}
        ],
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
