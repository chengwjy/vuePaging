<template>
  <div class="hello">
    
    <button v-for="item in pageItem" :key="item" class="pageItem" :class="{active:item == pageNow}" @click="$emit('pageCli',item);">
      {{item}}
    </button>
  </div>
</template>

<script>
import {generateArray} from '@/lib'
export default {
  name: 'paging',
  props: {
    config :{
      // 限定类型
      type:Object, 
    }
  },
  data(){
    return {
      pageNow: 0,
      pageItem:[]
    }
  },
  mounted(){

  },
  watch:{
    config:{
      handler(newValue,oldValue){
        console.log('分页配置更新',newValue)
        this.initPage()
      },
      deep:true
    },
  }
  ,
  methods:{
    // 渲染分页
    initPage(){
  
        if(!this.config.count){
          return false;
        }
        console.log('渲染分页')

        // 通过count/pageSize 计算pageCount(总页数)
        console.log('总数',this.config.count)
        console.log('偏移值',this.config.offset)
        console.log('一页数',this.config.pageSize)
        let pageCount = this.config.count % this.config.pageSize == 0 ?
                         Math.floor(this.config.count / this.config.pageSize) 
                         : Math.floor(this.config.count / this.config.pageSize) + 1
        console.log('总页数',pageCount)
        // 得到pageNow（当前页码
        
        let pageNow = this.config.offset === 0 ? 1 : this.config.offset / this.config.pageSize + 1
        console.log('当前页码',pageNow)

        let pageArr = []
        
        // 默认生成页码7个，当前页码默认在最中间
        if(pageNow - 3 > 0 && pageNow + 3 <= pageCount){
          pageArr = generateArray(pageNow - 3, pageNow + 3)
        }else if(pageNow - 3 > 0){
          pageArr = generateArray(pageCount > 7 ? pageCount - 7 :pageNow - 3, pageCount)
        }else if(pageNow + 3 <= pageCount){
          pageArr = generateArray(1, pageCount > 7 ? 7 : pageCount)
        }else{
          pageArr = generateArray(1, pageCount)
        }
        this.pageItem = pageArr
        this.pageNow = pageNow
        console.log('页码array',pageArr)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .pageItem{
    display: inline;
  }
  .pageItem.active{
    color:red
  }
</style>
