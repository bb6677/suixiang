<template>
  <div class="home">
    <div class="nav">
      <span
        @click="jump"
        style="
          font-size: 22px;
          color: cadetblue;
          margin-left: 10px;
          cursor: pointer;
        "
      >
        hello-7月</span
      >
      <p>{{ this.nowTime }}</p>
      <div class="nav_work">
        <p @click="haha" style="cursor: pointer">琉璃之金</p>
        <el-dropdown trigger="click">
          <span
            class="el-dropdown-link"
            style="font-size: 18px; color: rgb(243, 9, 231)"
          >
            朦胧之森<i class="el-icon-arrow-down el-icon--right"></i>
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item icon="el-icon-plus">黄金糕</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-plus"
              >狮子头</el-dropdown-item
            >
            <el-dropdown-item icon="el-icon-circle-plus-outline"
              >螺蛳粉</el-dropdown-item
            >
            <el-dropdown-item icon="el-icon-check">双皮奶</el-dropdown-item>
            <el-dropdown-item icon="el-icon-circle-check"
              >蚵仔煎</el-dropdown-item
            >
          </el-dropdown-menu>
        </el-dropdown>
        <p @click="xixi" style="cursor: pointer">飘渺之涛</p>
        <p @click="heihei" style="cursor: pointer">逍遥之火</p>
        <p @click="yoyo" style="cursor: pointer">璀璨之沙</p>
        <p @click="wowo" style="cursor: pointer">寒峭之雪</p>
      </div>
      <div class="jump_style">关于</div>
    </div>

    <div data-tname="WaveItem">
      <div class="main-container">
        <div class="waves">
          <div
            class="wave"
            v-for="(item, key) in waves"
            :key="key"
            :style="item"
          >
            <div
              v-for="n in wavesConfig.total"
              :key="n"
              class="wave-item"
              :style="{
                transform: `scale(${0.1 * Math.sqrt(n - 1)})`, // 使得波纹大小指数增长
                opacity: 0.3 * (1 / n), // 因为相互层叠的波纹透明度会相互叠加，需要越小的波纹透明度越低，以免中心颜色过重
                animationDelay: `${(n - 1) * 0.12}s`, // 越大的波纹越晚出现，以呈现波纹逐渐扩散的效果
                animationDuration: `${
                  0.6 + n * 0.3 + parseInt(item.width) * 0.002
                }s`, // 波纹动画时间渐增，表现波纹向外扩散渐慢的效果,波纹尺寸越大动画时间越长。
                backgroundColor: waveColor,
              }"
            ></div>
          </div>
        </div>
      </div>
    </div>
    <!-- 爱心子组件 -->
    <!-- <biglo></biglo> -->

    <div class="style_style"></div>
  </div>
</template>

<script>
// import biglo from '../components/Biglo.vue';
export default {
  // components: { biglo },
  name: "Home",
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",
      nowTime: "",
      waves: [],
      waveColor: "rgb(243, 9, 231)",
      wavesConfig: {
        maxSize: 300, // px，波纹最大尺寸
        minSize: 100, // px，波纹最小尺寸
        zIndexCount: 999, // 波纹父元素其z-index数值
        //波纹基础颜色
        total: 5, //波纹圈层数
      },
      clear: {
        delay: 5000,
        timeoutId: null,
      },
    };
  },
  mounted() {
    this.nowTimes();
    document.getElementById("app").onclick = (e) => {
      this.createWave(e);
      this.intervalClearWave();
    };
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
    jump() {
      this.$router.push({
        path: "/About",
      });
    },
    haha() {
      alert("朦胧之森");
    },
    xixi() {
      alert("飘渺之涛");
    },
    yoyo() {
      alert("璀璨之沙");
    },
    wowo() {
      alert("寒峭之雪");
      this.$router.push({
        path: "/Volume",
      });
    },
    heihei() {
      alert("逍遥之火");
    },
    //随机颜色
    rgb() {
      //rgb颜色随机
      var r = Math.floor(Math.random() * 256);
      var g = Math.floor(Math.random() * 256);
      var b = Math.floor(Math.random() * 256);
      var rgb = "(" + r + "," + g + "," + b + ")";
      this.waveColor = rgb;
      return rgb;
    },
    //获取系统时间
    getdate_show() {
      var date = new Date();
      var year = date.getFullYear();
      var month =
        date.getMonth() + 1 < 10
          ? "0" + (date.getMonth() + 1)
          : date.getMonth() + 1;
      var day = date.getDate() < 10 ? "0" + date.getDate() : date.getDate();
      var hh = date.getHours() < 10 ? "0" + date.getHours() : date.getHours();
      var mm =
        date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes();
      var ss =
        date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();
      this.nowTime =
        year + "-" + month + "-" + day + " " + hh + ":" + mm + ":" + ss;
    },
    nowTimes() {
      this.getdate_show();
      setInterval(this.nowTimes, 1000);
      this.clear1();
    },
    //清除日期定时器
    clear1() {
      clearInterval(this.nowTimes);
      this.nowTimes = null;
    },
    createWave(e) {
      // 让新生成的波纹始终在之前波纹的上层产生叠加效果
      if (this.wavesConfig.zIndexCount > 99999) {
        this.wavesConfig.zIndexCount = 999;
      } else {
        this.wavesConfig.zIndexCount++;
      }
      // 在一定范围内随机生成波纹的大小
      const waveSize = parseInt(
        Math.random() * (this.wavesConfig.maxSize - this.wavesConfig.minSize) +
          this.wavesConfig.minSize
      );
      //添加新的波纹数据
      this.waves.push({
        left: `${e.clientX - waveSize / 2}px`,
        top: `${e.clientY - waveSize / 2}px`,
        zIndex: this.wavesConfig.zIndexCount,
        width: `${waveSize}px`,
        height: `${waveSize}px`,
      });
    },
    intervalClearWave() {
      clearTimeout(this.clear.timeoutId);
      this.clear.timeoutId = setTimeout(() => {
        this.waves = [];
      }, this.clear.delay);
    },
  },
};
</script>
<style lang="less" scoped>
.home {
  /* background: url("../assets/背景2.jpg");
  width: 100%;
   height: 100%;
  position: fixed;
  background-size: 100% 100%; */
  position: relative;
  height: 100%;
}
.style_style {
  background-image: linear-gradient(#bcc7b8, #b5b9db);
  height: 200px;
}
.jump_style {
  background-color: rgb(224, 203, 105);
  position: fixed;
  right: 10px;
  bottom: 0;
  border-radius: 8px;
  color: rgb(243, 9, 231);
  font-size: 14px;
  cursor: pointer;
}
.nav {
  height: 50px;
  background-color: rgb(163, 207, 118);
  opacity: 0.5;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.nav_work {
  width: 55%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  font-size: 18px;
  color: rgb(243, 9, 231);
}
.waves {
  .wave {
    position: fixed;
    pointer-events: none; // 点击事件穿透，使得鼠标点击可以穿透波纹，兼容ie11及以上
    @keyframes wave {
      to {
        //波纹逐渐扩散变大变透明
        transform: scale(1);
        opacity: 0;
      }
    }
    .wave-item {
      width: 100%;
      height: 100%;
      position: absolute;
      border-radius: 100%;
      animation-name: wave;
      animation-fill-mode: forwards; // 动画结束后保持最后一帧的状态
      animation-timing-function: ease-out; // 波纹向外扩散渐缓
    }
  }
}
</style>
