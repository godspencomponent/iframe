
<template>
  <div class="hello">
    <div class="block">
      <div class="title">我是示例文本组件</div>
      <div class="node">
        <example></example>
      </div>
    </div>
    <div class="block">
      <div class="title">我是你正在开发的组件</div>
      <div class="node">
        <com></com>
      </div>
    </div>
    <toast ref='toast' :compromise="true"></toast>
    <loading ref="loading"></loading>
    <img-viewer ref="imgViewer"></img-viewer>
  </div>
</template>

<script>
import com from '../src/index'
import Loading from './components/Loading'
import example from '../src/example'
import ImgViewer from './components/ImgViewer'
import Toast from './components/Toast'
import MessageBox from 'mint-ui/message-box/'
import 'mint-ui/message-box/style.css'

export default {
  components: {Toast, Loading, ImgViewer, example, com},
  created () {
    var that = this
    window.msgBox = MessageBox
    window.alert = function (msg, fn) {
      MessageBox.close()
      var m, t
      if (typeof msg === 'object') {
        m = msg.msg
        t = msg.title
      } else {
        m = String(msg)
        t = '提示'
      }
      MessageBox.alert(m, t).then(action => {
        typeof fn === 'function' && fn(action)
      })
    }
    window.confirm = function (msg, fn, re) {
      MessageBox.close()
      var m, t
      if (typeof msg === 'object') {
        m = msg.msg
        t = msg.title
      } else {
        m = String(msg)
        t = '提示'
      }
      MessageBox.confirm(m, t).then(action => {
        typeof fn === 'function' && fn(action)
      }).catch(action => {
        typeof re === 'function' && re(action)
      })
    }
    window.prompt = function (msg, fn, re) {
      MessageBox.close()
      var m, t
      if (typeof msg === 'object') {
        m = msg.msg
        t = msg.title
      } else {
        m = String(msg)
        t = '提示'
      }
      MessageBox.prompt(m, t).then(val => {
        typeof fn === 'function' && fn(val)
      }).catch(action => {
        typeof re === 'function' && re(action)
      })
    }
    window.loading = function (hide) {
      if (!that.$refs['loading']) return
      if (!hide) that.$refs['loading'].open()
      else that.$refs['loading'].hide()
    }
    window.toast = function (msg, fn) {
      if (!that.$refs['toast']) return
      that.$refs['toast'].render({msg, fn})
    }
    window.viewImg = (imgs, index) => {
      if (!that.$refs.imgViewer) return
      that.$refs.imgViewer.open(imgs, index)
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus">
@require './style.css';

html,body  {
  margin: 0;
  padding: 0;
  width: 320px;
}
.block {
  min-height: 200px;
  margin-bottom: 20px;
  box-shadow: 0px 5px 10px 0px #ccc;
  background-color: #fff;
  .title {
    border-bottom: 1px solid #ccc;
    box-shadow: 0px -1px 10px 0px #ccc;
    color: #666;
    padding: 10px;
  }
}

</style>



