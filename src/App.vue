<template>
  <div id="app">
    <button @click="getHello">Get Hello</button>
    <p>{{ responseMessage }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      responseMessage: ''
    };
  },
  methods: {
    getHello() {
      // 发送GET请求到后端的"/hello"路径
      axios.get('http://localhost:8080/hello') // 请替换为你的后端地址和端口
        .then(response => {
          this.responseMessage = response.data;
        })
        .catch(error => {
          this.responseMessage = error;
          console.error('Error fetching hello:', error);
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
