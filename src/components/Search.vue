<template>
 <div>
    <el-row>
      <el-col :span="8" :offset="7">
        <el-input size="large" v-model="q" placeholder="请输入搜索内容" v-on:change="change" @keyup.enter.native='search' clearable></el-input>
      </el-col>
      <el-col :span="2">
        <el-button type="primary" v-on:click="search">搜索</el-button>
      </el-col>
    </el-row>
    <el-table class="table" v-if="tableData.length > 0" :data="tableData" stripe border style="width: 100%">
      <el-table-column prop="title" header-align="center" label="标题"></el-table-column>
      <el-table-column prop="link" header-align="center" label="链接" width="400px"></el-table-column>
      <el-table-column fixed="right" header-align="center" label="操作" width="150px">
        <template slot-scope="scope">
          <!-- <el-button @click="handleClick(scope.row)" type="text">查看</el-button> -->
          <el-button type="text">下载</el-button>
        </template>
      </el-table-column>
    </el-table>
 </div>
</template>

<script>
export default {
  name: 'search',
  data () {
    return {
      q: '',
      tableData: []
    }
  },
  methods: {
    search: async function () {
      let res = await this.$ajax.get(`http://207.148.65.173:3000/search?q=${this.q}`)
      this.tableData = res.data || []
    },
    change: async function (value) {
      if (value.length === 0) this.tableData = []
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.table {
  margin-top: 40px;
}
</style>
