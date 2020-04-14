<template>
  <div class="scrollboard-list" @mouseenter="enter = true" @mouseleave="enter = false">
    <div class="change-btn btn-left" v-show="enter" @click="move(1)">
      <i class="scroll-arrow-left"></i>
    </div>
    <div class="change-btn btn-right" v-show="enter" @click="move(2)">
      <i class="scroll-arrow-right"></i>
    </div>

    <div class="list-container" :class="{'ani':isAni}" :style="{left:goLeft+'px'}">
      <div v-for="(item, index) in 3" :key="index" class="loop-box">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
import { throttle } from '../utils/tools'
export default {
  data() {
    return {
      len: 5,
      black: 5,
      isAni: true,
      goLeft: -420 * 5,
      enter: false
    }
  },
  methods: {
    resetPosition(type) {
      this.isAni = false
      this.goLeft = -420 * 5

      setTimeout(() => {
        this.isAni = true
        this.moveFn(type)
      }, 500)
    },
    moveFn(type) {
      let scrollWidth = 420 //每次滚动的宽度
      let showNumber = 5 //看得见的数量
      // eslint-disable-next-line no-debugger
      if (type == 1) {
        this.black = Math.abs(this.goLeft) / scrollWidth - 1
        if (this.goLeft != 0) {
          this.goLeft += scrollWidth
        } else {
          this.resetPosition(type)
        }
      }
      if (type == 2) {
        this.black = Math.abs(this.goLeft) / scrollWidth + 1
        let leftSet = (this.len * 3 - showNumber) * scrollWidth
        if (Math.abs(this.goLeft) < leftSet) {
          this.goLeft -= scrollWidth
        } else {
          this.resetPosition(type)
        }
      }
      console.log('black', this.black)
    },
    move: throttle(this.moveFn, 500, 1)
  }
}
</script>

<style>
.scrollboard-list {
  width: 100%;
  height: 240px;
  overflow: hidden;
  position: relative;
}
.scrollboard-list > .list-container {
  display: flex;
  display: -webkit-flex;
  position: absolute;
  transform: translateX(-107px);
}

.scrollboard-list > .ani {
  transition: left 0.5s ease-in-out;
}
.scroll-arrow-left {
  font-family: element-icons !important;
  speak: none;
  font-style: normal;
  font-weight: 400;
  font-variant: normal;
  text-transform: none;
  line-height: 1;
  vertical-align: baseline;
  display: inline-block;
  -webkit-font-smoothing: antialiased;
}
.scroll-arrow-right {
  font-family: element-icons !important;
  speak: none;
  font-style: normal;
  font-weight: 400;
  font-variant: normal;
  text-transform: none;
  line-height: 1;
  vertical-align: baseline;
  display: inline-block;
  -webkit-font-smoothing: antialiased;
}
.change-btn {
  position: absolute;
  width: 35px;
  height: 92px;
  background: rgba(0, 0, 0, 1);
  opacity: 0.8;
  z-index: 2;
  top: calc(50% - 46px);
}
.change-btn > i {
  margin: 38px 10px;
  color: #fff;
  cursor: pointer;
}
.btn-left {
}
.btn-right {
  right: 0;
}
.loop-box {
  display: inherit;
}
</style>