<template>
  <div class="main">
    <div class="disc1"></div>
    <div class="disc2"></div>
    <div class="square"></div>
  </div>
</template>
<script>
export default {
  name: "Biglo",
  date() {
    return {};
  },
};
</script>
<style lang="less" scoped>
.main {
  transform: rotate(45deg);
  margin: 300px;
}
.disc1 {
  width: 100px;
  height: 100px;
  border: 1px solid red;
  background-color: red;
  margin: 300px 0px 0px 300px;
  border-radius: 100%;
  float: left;
}
.disc2 {
  width: 100px;
  height: 100px;
  border: 1px solid red;
  background-color: red;
  margin: 250px 0px 0px 0px;
  border-radius: 100%;
  float: left;
  position: relative;
  right: 50px;
}
.square {
  width: 100px;
  height: 100px;
  border: 1px solid red;
  background-color: red;
  margin: 300px 0px 0px 0px;
  float: left;
  position: relative;
  right: 152px;
}
</style>
