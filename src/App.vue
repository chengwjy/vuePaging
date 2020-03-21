<template>
  <div id="app">

    <ul>
      <li v-for="item in goods" :key="item">
        {{item}}
      </li>
    </ul>
    <Paging :config="page" @pageCli="pageCli"></Paging>
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
      // 商品列表
      goods: [],
      // 分页参数
      page:{
        count: 0,
        pageSize: 0,
        offset: 0
      }
    }
  },

  mounted(){
    let that = this
    axios.get('http://mock/api/hello')
      .then(function (response) {
      
        //将app2中双向绑定的msg数据更改为mock模拟数据
        that.page =  response.data.data.config
        that.goods = response.data.data.goods
        // console.log( response)
      })
      .catch(function (error) {
        console.log(error);
      });
  },
  methods: {
    pageCli(item){
      console.log('子组件点击页码',item)
    }
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
