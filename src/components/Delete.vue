<template>
  <el-button type="text" class="link" @click="open">删除本站偏好设置</el-button>
</template>

<script>
export default {
  name: 'delete',
  mounted() {
    // console.log(JSON.parse(localStorage.sites));
  },
  data() {
    return {
    };
  },
  methods: {
    open() {
      this.$confirm('此操作将清除您在本站的偏好设置记忆，并且无法恢复。是否继续?', '危险操作提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'error',
      }).then(() => {
        localStorage.clear();
        this.$message({
          type: 'success',
          message: '删除成功!',
        });
        location.href = '/';
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@media (min-width: 768px) {
  .setup {
    position: absolute;
    right: 16px;
    top: 8px;
  }
}
@media (max-width: 768px) {
  .setup {
    position: absolute;
    right: 4px;
    top: 4px;
  }
}
.link {
  color: #f56c6c;
}
.link:hover {
  color: #fbc4c4;
}
</style>
