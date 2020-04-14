<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <scrollboard>
      <scrollboard-item v-for="(item, index) in latest" :key="index" class="latest-box">
        <div class="box-title">{{item.title}}</div>
        <div class="bottom">
          <span>{{item.time}}</span>
          <span style="margin-left:22px">{{item.location}}</span>
        </div>
      </scrollboard-item>
    </scrollboard>
  </div>
</template>

<script>
import scrollboard from '../src/components/board'
import scrollboardItem from '../src/components/item'
export default {
  name: 'App',
  components: {
    scrollboard,
    scrollboardItem
  },
  data() {
    return {
      latest: [
        {
          title: '2019全国工业互联网产业联盟大会1',
          time: '2019.12.06',
          location: '贵阳'
        },
        {
          title: '2019全国工业互联网产业联盟大会2',
          time: '2019.12.06',
          location: '贵阳'
        },
        {
          title: '2019全国工业互联网产业联盟大会3',
          time: '2019.12.06',
          location: '贵阳'
        },
        {
          title: '2019全国工业互联网产业联盟大会4',
          time: '2019.12.06',
          location: '贵阳'
        },
        {
          title: '2019全国工业互联网产业联盟大会5',
          time: '2019.12.06',
          location: '贵阳'
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.latest-box {
  border: 1px solid #eee;
  cursor: pointer;
  display: inline-block;
  width: 360px;
  height: 240px;
  margin: 0 30px;
  position: relative;
}
.latest-box > .box-title {
  margin: auto;
  height: 65px;
  font-size: 24px;
  font-family: Microsoft YaHei;
  font-weight: bold;
  color: #333;
}
.latest-box > .bottom {
  margin-top: 45px;
  font-size: 16px;
  font-family: Microsoft YaHei;
  font-weight: 400;
  color: #333;
}
</style>
