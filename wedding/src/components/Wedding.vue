<template>
  <div class="content">
    <div class="wedding-wrap">
      <header class="editor-header">
        <a href="javascript:;"></a>
        <a href="javascript:;" class="minimum"></a>
        <a href="javascript:;" class="maximum"></a>
      </header>
      <button @click="start">start</button>
      <p class="code">Last login: <span>{{ today }}</span> on admin</p>
      <pre>
        <div class="code">{{currentCode}}<span style="opacity:${this.showCursor}"> ▍</span></div>
      </pre>
    </div>
  </div>
</template>

<script>
import data from '../assets/data'
export default {
  name: 'Wedding',
  props: {
    msg: String
  },
  data() {
    return {
      today: '',
      timer: 0, //计时
      typingCount: 0, //打字计数
      currentCode:'', //显示文字
      code: data.code, //全部文字
      showCursor: 1,
      showInvitation: true
    }
  },
  created() {
    this.today = (new Date()).toDateString()
    // this.start()
  },
  methods: {
    start() {
      this.startTyping()
    },
    startTyping() {
      if (this.typingCount > this.code.length) {
        window.cancelAnimationFrame(this.timer);
        console.log("end")
      } else {
        let randomNumber = Math.round(Math.random() * 6)
        if(this.timer % 2 === 0 && randomNumber % 4 === 0){
          this.currentCode = this.code.substring(0, this.typingCount)
          this.typingCount++
        }
        if(this.timer % 24 === 0){
          this.showCursor = this.showCursor === 0 ? 1 : 0
        }
        this.timer = window.requestAnimationFrame(this.startTyping);
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.content {
  display: flex;
  justify-content: center;
}
.wedding-wrap{
  position: absolute;
  width: 568px;
  height: 100%;
  padding: 15px;
  overflow-x: hidden;
  overflow-y: auto;
  z-index: 1;
  background: #2B2B48;
  .editor-header{
    position: absolute;
    left: 0;
    top: 0;
    width: 568px;
    padding: 12px;
    overflow: hidden;
    background: #2B2B48;
    z-index: 3;
    >a{
      float: left;
      display: block;
      width: 16px;
      height: 16px;
      margin-right: 5px;
      border-radius: 8px;
      background: #FC615D;
      &.minimum{
        background: #FDBC40;
      }
      &.maximum{
        background: #34C84A;
      }
    }
  }
  p.code{
    margin-left: 20px;
    color: #bbbbbb;
    line-height: 1.2;
    font-family: 'Roboto Mono', 'microsoft Yahei', 'Monaco', Courier, monospace !important;
    font-weight: 500 !important;
    font-size: 16px!important;
  }
  pre{
    margin: 0;
    white-space: pre-wrap;
    .code{
      white-space: pre-wrap;
      word-break: break-all;
      font-size: 16px!important;
      margin: 0;
      color: antiquewhite;
      line-height: 1.5;
      font-family: 'Roboto Mono', 'microsoft Yahei', 'Monaco', Courier, monospace !important;
      font-weight: 500 !important;
      background: transparent;
    }
  }
}
</style>
