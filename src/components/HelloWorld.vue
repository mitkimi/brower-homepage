<template>
  <el-container class='container'>
    <Setup @flushSites="loadSites" />
    <div class="box-card">
      <div class="endui">
        <img src="@/assets/endui.png" />
      </div>
      <div slot="header" class="clearfix">
        <div class="input-with-select">
          <el-input
            placeholder="请输入内容"
            v-model="search.txt"
            @keyup.native="autoSearch"
            autofocus
          >
            <el-select
              v-model="search.choose"
              slot="prepend"
              placeholder=""
              @change="setDefaultSearch">
              <el-option label="Google" value="google"></el-option>
              <el-option label="百度" value="baidu"></el-option>
            </el-select>
            <el-button slot="append" icon="el-icon-search" @click="goSearch"></el-button>
          </el-input>
        </div>
      </div>
      <div v-for="o in sites" :key="o.key" class="main-box" style="padding-top: 40px;">
        <div class="style-title">{{ o.title }}</div>
        <el-row :gutter="20">
          <Site v-for="p in o.sites" :key="p.key" :data="p" v-if="p.checked === true" />
        </el-row>
      </div>
    </div>
  </el-container>
</template>

<script>
import Setup from '@/components/Setup';
import Site from '@/components/Site';

export default {
  name: 'HelloWorld',
  components: { Setup, Site },
  created() {
    if (!localStorage.sites) {
      const defaultSites = [
        {
          key: 'developer',
          title: '开发者/设计师',
          sites: [
            {
              key: 11,
              name: '语雀',
              avatar: 'yuque.png',
              link: 'https://www.yuque.com/',
              checked: true,
            },
            {
              key: 12,
              name: 'GITLAB',
              avatar: 'gitlab.png',
              link: 'https://gitlab.ipietech.com',
              checked: true,
            },
            {
              key: 13,
              name: 'GITHUB',
              avatar: 'github.png',
              link: 'https://github.com',
              checked: true,
            },
            {
              key: 14,
              name: 'ICONFONT',
              avatar: 'iconfont.png',
              link: 'https://www.iconfont.cn/',
              checked: true,
            },
            {
              key: 15,
              name: 'UNSPLASH',
              avatar: 'unsplash.png',
              link: 'https://unsplash.com/',
              checked: true,
            },
          ],
        },
      ];
      localStorage.sites = JSON.stringify(defaultSites);
    }
  },
  mounted() {
    // console
    if (localStorage.sites) {
      this.loadSites();
    }
  },
  data() {
    return {
      search: {
        choose: localStorage.choose || 'google',
        txt: '',
      },
      sites: [],
    };
  },
  methods: {
    setDefaultSearch() {
      // eslint-disable-next-line
      this.$message.success(`已为您设定默认搜索引擎为 ${this.search.choose}`);
      localStorage.choose = this.search.choose;
    },
    goSearch() {
      const base = !localStorage.choose || this.search.choose === 'google' ? 'https://www.google.com/search?q=' : 'https://www.baidu.com/s?wd=';
      if (!this.search.txt) {
        this.$message.error('请输入搜索关键字');
        return false;
      }
      window.open(`${base}${this.search.txt}`);
      return false;
    },
    autoSearch(ev) {
      if (ev.keyCode === 13) {
        this.goSearch();
      }
      return false;
    },
    loadSites(sites) {
      if (sites) {
        // this.$message.success('调用到了');
        this.sites = sites;
      } else {
        this.sites = JSON.parse(localStorage.sites);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

@media (min-width: 768px) {
  .style-title {
    margin-bottom: 40px;
  }
  .box-card {
    width: 100%;
    padding: 0 0 40px 0;
    margin-top: 100px;
  }
  .input-with-select {
    width: 600px;
    margin: 0 auto 40px auto;
  }
  .el-select {
    width: 100px;
  }
  .endui {
    font-size: 48px;
    color: #333333;
    text-align: center;
    margin-bottom: 40px;
  }
}
@media (max-width: 768px) {
  .style-title {
    margin-bottom: 20px;
  }
  .main-box {
    margin: 0 20px;
  }
  .box-card {
    width: 100%;
    padding: 40px 0 40px 0;
  }
  .input-with-select {
    margin: 0 auto 40px auto;
    padding: 0 20px;
  }
  .el-select {
    width: 100px;
  }
  .endui {
    font-size: 40px;
    color: #333333;
    text-align: center;
    margin-bottom: 20px;
  }
}


</style>
