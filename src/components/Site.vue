<template>
  <el-col class="site-box" :xs="12" :sm="6" :md="6" :lg="4" :xl="4">
    <div class="box" @click="goLink">
      <div class="my-card" shadow="hover">
        <img :src="img" />
      </div>
      <div class="title">
        {{ name }}
      </div>
    </div>
  </el-col>
</template>
<script>
export default {
  name: 'Site',
  props: ['data'],
  data() {
    return {
      name: this.data.name,
      // eslint-disable-next-line
      img: require('../assets/' + this.data.avatar),
    };
  },
  mounted() {},
  methods: {
    goLink() {
      window.open(this.data.link);
    },
  },
};
</script>

<style scoped>
@media (min-width: 768px) {
  .my-card {
    width: 100px;
    height: 100px;
    margin: 0 auto;
    border-radius: 10px;
    border: 1px solid #ebeef5;
    background-color: #fff;
    -webkit-box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
    box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
  }
  .my-card img {
    width: 100%;
    height: 100%;
  }
  .title {
    font-size: 16px;
    color: #262626;
    margin-top: 15px;
    text-align: center;
    letter-spacing: 1.8;
    font-family: PingFangSC-Regular;
  }
  .box {
    cursor: pointer;
  }
  .site-box {
    margin-bottom: 60px;
  }
  .el-card {
    padding: 0!important;
  }
}
@media (max-width: 768px) {
  .my-card {
    width: 40px;
    height: 40px;
    margin: 0 auto;
    border-radius: 10px;
    border: 1px solid #ebeef5;
    background-color: #fff;
    -webkit-box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
    box-shadow: 0 2px 12px 0 rgba(0,0,0,.1);
    float: left;
  }
  .my-card img {
    width: 100%;
    height: 100%;
  }
  .title {
    font-size: 16px;
    color: #262626;
    line-height: 40px;
    margin-left: 14px;
    text-align: center;
    letter-spacing: 1.8;
    font-family: PingFangSC-Regular;
    float: left;
  }
  .title:after {
    clear: both;
  }
  .box {
    cursor: pointer;
  }
  .site-box {
    margin-bottom: 28px;
  }
  .el-card {
    padding: 0!important;
  }
}
</style>
