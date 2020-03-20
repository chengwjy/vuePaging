<template>
  <div id="app">
    <Paging :config="page"></Paging>
  </div>
</template>

<script>

import axios from 'axios'
import Paging from './components/Paging.vue'

export default {
  name: 'App',
  components: {
    Paging
  },
  data(){
    return {
      page:{
        1:1
      }
    }
  },
  mounted(){

axios.get('http://mock/api/hello')
  .then(function (response) {
    console.log(response);
    //将app2中双向绑定的msg数据更改为mock模拟数据
    
  })
  .catch(function (error) {
    console.log(error);
  });

  }
}
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
