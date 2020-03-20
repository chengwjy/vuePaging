<template>
  <div class="hello">
    paging
  </div>
</template>

<script>
export default {
  name: 'paging',
  props: {
    config :{
      // 限定类型
      type:Object,
      // 默认值(父组件未传值)
      default(){
          // 这里为什么要用工厂函数？思考下，当限定类型为Object或Array时会报错
          return ['不能说的秘密','头文字D'];
      },
  }
  },
  mounted(){
    console.log(this.config)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
