<template lang="pug">
  div
    div.progress(v-if="showProcess" :style="{width:width+'px'}")
      span <span>{{currentTime}}</span> / {{time}}
      process(:time="time*1000")
    span.noProcess(v-else) {{currentTime}}
</template>
<script>
import process from './process'
export default {
  name: 'countdown',
  components: { process },
  props: {
    time: 0,
    showProcess: {
      default: false
    },
    width: {
      default: 456
    }
  },
  data () {
    return {
      currentTime: 0,
      flag: ''
    }
  },
  methods: {
    countdown (time) {
      clearTimeout(this.flag)
      this.currentTime = time
      if (time <= 0) {
        this.$emit('end')
      } else {
        this.flag = setTimeout(() => {
          this.countdown(time - 1)
        }, 1000)
      }
    }
  },
  mounted () {
    this.countdown(this.time)
  },
  destroyed () {
    clearTimeout(this.flag)
  },
  watch: {
    time (v) {
      this.countdown(v)
    }
  }
}
</script>
<style lang="less" scoped>
.hidden {
  display: none !important;
}
.noProcess {
  color: #fff;
  font-size: 30px;
  font-weight: bold;
}
.progress {
  position: relative;
  width: 100%;
  height: 14px;
  background: #53cc92;
  border-radius: 7px;

  & > span {
    position: absolute;
    top: -24px;
    left: 50%;
    color: #fff;
    font-size: 16px;
    transform: translateX(-50%);

    span {
      color: #fbc564;
      font-size: 16px;
    }
  }
  // .countdown_peocess {
  //   animation: countdown linear forwards;
  // }
  // @keyframes countdown {
  //   to {
  //     width: 100%;
  //   }
  // }
}
</style>

