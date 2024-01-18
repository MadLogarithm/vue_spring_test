<template>
  <div id="app">
    <button @click="getHello">Get Hello</button>
    <p>{{ responseMessage1 }}</p>
    <button @click="getUser">Get User(init test)</button>
    <el-table :data="tableData" stripe style="width: 100%">
      <el-table-column prop="id" label="id" width="180"></el-table-column>
      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="email" label="邮箱"></el-table-column>
    </el-table>
    <el-input v-model="selectId" placeholder="请输入内容" clearable>
      <el-button slot="append" icon="el-icon-search" @click="selectUser"></el-button>
    </el-input>
    <el-table :data="userData" stripe style="width: 100%">
      <el-table-column prop="id" label="id" width="180"></el-table-column>
      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="age" label="年龄"></el-table-column>
    </el-table>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      responseMessage1: 'null',
      responseMessage2: 'null',
      responseMessage3: 'null',
      selectId: null,
      tableData: [],
      userData: []
    };
  },
  methods: {
    getHello() {
      // 发送GET请求到后端的"/hello"路径
      axios.get('http://localhost:8080/hello') // 请替换为你的后端地址和端口
          .then(response => {
            this.responseMessage1 = response.data;
          })
          .catch(error => {
            this.responseMessage1 = error;
            console.error('Error fetching hello:', error);
          });
    },
    getUser() {
      // 发送GET请求到后端的"/hello"路径
      axios.get('http://localhost:8080/getUser') // 请替换为你的后端地址和端口
        .then(response => {
          this.responseMessage2 = response.data;
          this.tableData = this.parseData(response.data);
        })
        .catch(error => {
          this.responseMessage2 = error;
          console.error('Error fetching getUser:', error);
        });
    },
    selectUser() {
      axios.get(`http://localhost:8080/user/${this.selectId}`)
          .then(response => {
            this.userData = response.data;
          })
          .catch(error => {
            this.responseMessage3 = error;
            console.error('Error fetching user:', error);
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
