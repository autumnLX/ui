<template lang="pug">
  div.line
    //- 使用ms更精确
    div.countdown_peocess(:style='{width:width + "%"}') 
</template>

<script>
export default {
  props: ['time'],
  data () {
    return {
      width: 0,
      _width: 0,
      currenttime: 0,
      flag: ''
    }
  },
  methods: {
    countdown () {
      clearInterval(this.flag)
      // 不用css动画，浏览器切出去时css3可能会停止
      this.flag = setInterval(() => {
        if (this.currenttime > this.time + 30) {
          clearInterval(this.flag)
        } else {
          this.currenttime = this.currenttime + 30
          this._width = this.currenttime / this.time * 100
          this.width = this._width >= 100 ? 100 : this._width
        }
      }, 30)
    }
  },
  mounted () {
    this.countdown()
  },
  watch: {
    time (v) {
      this.countdown()
    },
  },
  destroyed () {
    clearInterval(this.flag)
  }
}
</script>

<style lang="less" scoped>
.line {
  position: relative;
  width: 100%;
  height: 14px;
  background: #53cc92;
  border-radius: 7px;
  div {
    position: absolute;
    top: 0;
    left: 0px;
    width: 0;
    height: 14px;
    background: #fff;
    transition-property: width;
    transition-timing-function: linear;
    border-radius: 7px;
  }
}
</style>
