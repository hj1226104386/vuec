<template>
  <div id="documentPreview">
    <iframe :src="url" frameborder="0"></iframe>
  </div>
</template>

<script>
  export default {
    name: 'documentPreview',
    data () {
      return {
        url: this.$store.getters.getDocumentUrl // getters相当于computed计算属性，store中值改变自动更新
      }
    }
  }
</script>


<style scoped lang='scss'>
  #documentPreview {
    width: 100%;
    height: 100%;
    iframe {
      width: 100%;
      height: 100%;
    }
  }
</style>
