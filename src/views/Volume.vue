<template>
  <div>
    <div class="xue">滚动图</div>
    <el-carousel :interval="interval" type="card" height="500px">
      <el-carousel-item v-for="item in imgList" :key="item.id">
        <!-- <h3 class="medium">{{ item }}</h3> -->
        <img class="img_style" :src="item.idView" alt="" />
      </el-carousel-item>
    </el-carousel>
    <div :interval="interval" v-for="i in textList" :key="i.id">
      <p>{{ i.text }}</p>
    </div>
    <el-tooltip v-if="show" content="走你" placement="top">
      <el-button
        v-if="show"
        @click="tab"
        type="success"
        icon="el-icon-sunrise-1"
        style="font-size: 28px"
        circle
      ></el-button>
    </el-tooltip>
    <el-tooltip v-if="!show" content="停下" placement="top">
      <el-button
        v-if="!show"
        @click="tab1"
        type="warning"
        icon="el-icon-moon-night"
        style="font-size: 28px"
        circle
      ></el-button>
    </el-tooltip>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: true,
      interval: 2000,
      imgList: [
        { id: 0, idView: require("../assets/imgList/背景.png") },
        { id: 1, idView: require("../assets/imgList/背景2.jpg") },
        { id: 2, idView: require("../assets/imgList/背景.png") },
        { id: 3, idView: require("../assets/imgList/背景2.jpg") },
        { id: 4, idView: require("../assets/imgList/背景.png") },
        { id: 5, idView: require("../assets/imgList/背景2.jpg") },
      ],
      textList: [
        { id: 0, text: "123" },
        { id: 1, text: "456" },
        { id: 2, text: "789" },
        { id: 3, text: "789" },
      ],
    };
  },
  methods: {
    tab() {
      this.show = !this.show;
      this.interval = null;
      alert(window.location)
    },
    tab1() {
      this.show = !this.show;
      this.interval = 2000;
    },
  },
};
</script>
<style lang="less" scoped>
.xue {
  font-size: 30px;
  color: aquamarine;
  height: 100%;
//   background-image: linear-gradient(#c0e79c, #a5e6e2);
//   background-size: 100% 100%;
//   background-repeat: no-repeat;
}
.el-carousel__item h3 {
  color: #475669;
  font-size: 14px;
  opacity: 0.75;
  line-height: 200px;
  margin: 0;
}
.img_style {
  width: 100%;
  height: 100%;
}
.el-carousel__item:nth-child(2n) {
  background-color: #99a9bf;
}

.el-carousel__item:nth-child(2n + 1) {
  background-color: #d3dce6;
}
</style>
