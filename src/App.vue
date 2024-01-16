<template>
  <div id="app">
    <button @click="getHello">Get Hello</button>
    <p>{{ responseMessage }}</p>
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="id" label="id" width="180"></el-table-column>
      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="email" label="邮箱"></el-table-column>
    </el-table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      responseMessage: '',
      tableData: []
    };
  },
  methods: {
    getHello() {
      // 发送GET请求到后端的"/hello"路径
      axios.get('http://localhost:8080/getUser') // 请替换为你的后端地址和端口
        .then(response => {
          this.responseMessage = response.data;
          this.tableData = this.parseData(response.data);
        })
        .catch(error => {
          this.responseMessage = error;
          console.error('Error fetching hello:', error);
        });
    },
    parseData(data) {
      return data.map(item => {
        return {
          id: item[0],
          name: item[1],
          email: item[2]
        };
      });
    }
  }
};
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
</style>
