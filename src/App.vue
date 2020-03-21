<template>
  <div id="app">
    <input type="text" v-model="keyword">
    <ul>
      <li v-for="item in goods" :key="item.server">
        {{item.server}}
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
      keyword: '',
      // 商品列表
      goods: [],
      // 分页参数
      page:{
        count: 0,
        pageSize: 12,
        offset: 0
      }
    }
  },

  mounted(){

  },
  methods: {
    rush(){
      let that = this
      axios.get('http://www.fengxiangqu.com/images/CApi.php?action=brand_category_info',
        {
          params:{
          'offset' : this.page.offset,
          'count' : this.page.pageSize,
          'keyword': this.keyword
        }
      })
      .then(function (res) {
          if(res.data.err_code == 0){
            let data = res.data.data;
            that.page.count = data.count
            that.goods = data.data
            console.log(that.goods)
          }
      })
      .catch(function (error) {
         console.log(error);
       });
    },

    pageCli(item){
      // 计算出offset继续
      console.log('子组件点击页码',item)
      this.page.offset = (item - 1) * this.page.pageSize
      this.rush()
    }
  },
  watch:{
    keyword:function(v){
      console.log('赋值关键词继续')
      this.rush()
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
