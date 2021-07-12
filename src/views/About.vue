<template>
  <div class="about">
    <h1>7月小新本</h1>
    <div>
      <img
        class="img_playmusic"
        src="../assets/placeholder_disk_play_song.png"
        alt=""
      />
    </div>
    <div class="lyrics">
      <p>
        去微软推哦怕时代法国红酒看来自行车v吧阿斯顿豆腐干豆腐干的风格更好的风格和啊实打实大方式
        给对方速度还是是符合法规和地方偶尔民风民俗调查阿斯顿挖的我没法v给阿斯顿买哪个竞女个人的撒大苏打发生的
      </p>
    </div>
    <div class="progress">
      <span>{{ this.start }}</span>
      <el-progress
        class="progress_bar"
        style="width: 50%"
        
        :percentage="50"
      ></el-progress>
      <span>{{this.end}}</span>
    </div>
    <div class="operating">
      <audio :src="audiourl"></audio>
      <img style="height: 50px" src="../assets/pre_l.png" alt="" />
      <img
        v-if="show"
        style="height: 70px"
        @click="stop"
        src="../assets/play.png"
        alt=""
      />
      <img
        v-else
        @click="stop"
        style="height: 70px"
        src="../assets/pause.png"
        alt=""
      />
      <img  style="height: 50px" src="../assets/pre_r.png" alt="" />
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      audiourl: "",
      show: true,
      isOk:true,
      start: '00.00',
      end: '01.00',
      second: 0, //秒
      minute: 0,
      time: "",
      count:0,
    };
  },
  methods: {
    // format(percentage) {
    //   return percentage === 100 ? "" : ((Number(this.end)-Number(this.start))/Number(this.end));
    // },
    stop() {
     this.show = !this.show;
      if (this.isOk&&this.show==false) {
        this.timeStart();
      } else {
        clearTimeout(this.time);
      }
       
    },
    timeStart() {
      this.time = setInterval(this.timer, 1000);

    },
    timer() {
      if (this.second >= 60) {
        this.second = 0;
        this.minute = this.minute + 1; //分钟
      }
      this.second++

      console.log(this.second);
      this.start = this.toDub(this.minute) + ":" + this.toDub(this.second);
    },
    toDub(n) {
      if (n < 10) {
        return "0" + n;
      } else {
        return "" + n;
      }
    },
    timeStop() {
      clearTimeout(this.time);
    },
  },
};
</script>
<style lang="less"  scoped>
.about {
  background-image: linear-gradient(#e66465, #9198e5);
  background-size: 100% 100%;
  background-repeat: no-repeat;
}
.img_playmusic {
  height: 300px;
  margin-top: 45px;
  border-radius: 100%;
}
.operating {
  display: flex;
  justify-content: center;
  align-items: center;
  img {
    margin: 0 50px;
  }
}
.progress {
  margin: 30px 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.lyrics {
  margin: 0 auto;
  height: 200px;
  width: 10%;
  overflow-y: auto;
  overflow-x: hidden;
  word-wrap: break-word;
  word-break: break-all;

  p {
    line-height: 30px;
  }
}
::-webkit-scrollbar {
  width: 2px;
  /*height: 4px;*/
  //background-color: rgb(240, 200, 234);
}
::-webkit-scrollbar-track {
  border-radius: 10px;
}

/* 滚动条滑块 */
::-webkit-scrollbar-thumb {
  border-radius: 10px;
 // background: rgb(214, 174, 128);
}
</style>

