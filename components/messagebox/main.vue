<template lang="pug">
  div.layer(@click.self="close" v-if="visiable")
    div.content(:class="{center:iscenter}")
      div
        i.iconfont.toast(:class="type") &#xe6b3;
      i.iconfont.close(@click.self="close") &#xe60a;
      div
        slot
          p.title(v-if="!useHtml") {{title}}
          p.desc(v-if="!useHtml") {{desc}}
          p.title(v-if="useHtml" v-html="title")
          p.desc(v-if="useHtml" v-html="desc")
      div.button(v-if="showButton")
        kmbutton(@click="confirm" type=normal :isBack="true") {{confirmTxt}}
        kmbutton(@click="cancel" v-if="showCancelButton") {{cancelTxt}}
      div(v-if="showCancelButton")
        span 不再提醒
</template>

<script>
import Kmbutton from '../button/main'
export default {
  components: { Kmbutton },
  methods: {
    close () {
      this.$destroy()
      this.$el.parentElement.removeChild(this.$el)
    },
    confirm () {
      this.callback()
      this.close()
    },
    cancel () {
      this.cancelCall()
      this.close()
    }
  },
  data () {
    return {
      cancelCall: '',
      callback: '',
      confirmTxt: '',
      cancelTxt: '',
      iscenter: '',
      showButton: '',
      type: '',
      title: '',
      desc: '',
      useHtml: '',
      showCancelButton: '',
      visiable: ''
    }
  },
  mounted () {
    this.$nextTick(() => {
      this.visiable = true
    })
  }
}
</script>
<style lang="less" scoped>
*{
  margin: 0;
  padding: 0;
}
.layer {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 100;
  .close {
    position: absolute;
    font-size: 20px;
    top: 6px;
    right: 6px;
    cursor: pointer;
  }
  background: rgba(0, 0, 0, 0.6);
  .content {
    background: #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    min-height: 270px;
    min-width: 400px;
    padding: 20px;
    box-sizing: border-box;
    border-radius: 4px;
  }
  .content.center {
    text-align: center;
  }
  .button {
    display: flex;
    margin-top: 20px;
    justify-content: center;
  }
  i.error {
    color: #ff6666;
  }
  i.warn {
    color: wheat;
  }
  i.toast {
    font-size: 60px;
  }
  .title{
    font-size: 18px;
    color: #333;
  }
  .desc{
    margin-top: 20px;
    font-size: 14px;
    color: #666;
  }
}
</style>


