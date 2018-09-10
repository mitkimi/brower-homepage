<template>
  <div class="setup">
    <el-button icon="el-icon-setting" size="small" @click="dialogVisible = true" plain>
      设置
    </el-button>
    <el-dialog
      title="快捷设置"
      :visible.sync="dialogVisible"
      class="dialog"
      width="80%">
      <div>
        <el-alert
          title="请勾选您常用的网站，他们将显示在首页上。"
          type="info"
          :closable="false">
        </el-alert>
        <el-card v-for="o in sites" :key="o.key" class="box-card">
          <div slot="header" class="clearfix">
            <span>{{ o.title }}</span>
          </div>
          <div style="padding-top: 10px;">
            <el-row :gutter="20">
              <el-col
                :span="4"
                :xs="12"
                v-for="p in o.sites"
                :key="p.key"
                style="margin-bottom: 10px">
                <el-checkbox v-model="p.checked">{{ p.name }}</el-checkbox>
              </el-col>
            </el-row>
          </div>
        </el-card>

        <div style="margin-top: 20px;">
          <Delete />
        </div>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="save">保 存</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import Delete from './Delete';

export default {
  name: 'setup',
  components: { Delete },
  created() {
    this.sites = JSON.parse(localStorage.sites);
  },
  mounted() {
    // console.log(JSON.parse(localStorage.sites));
  },
  data() {
    return {
      dialogVisible: false,
      sites: [],
    };
  },
  methods: {
    save() {
      localStorage.sites = JSON.stringify(this.sites);
      this.dialogVisible = false;
      this.$message.success('保存成功！');
      this.$emit('flushSites', this.sites);
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
.box-card {
  margin-top: 16px;
}
</style>
