<template>
  <div class="search-input">
    <form>
      <input type="search" :placeholder='placeHolder' autocomplete="off" :keyup.enter='serialize'
             v-model='searchValue'>
    </form>
    <i class='iconfont icon-search' @click='serialize'></i>
  </div>
</template>

<script>
  export default {
    name: 'searchInput',
    props: ['inputValue', 'placeHolder'],
    data () {
      return {
        searchValue: ''
      }
    },
    methods: {
      serialize: function () {
        this.$emit('update:text', this.searchValue)
      }
    }
  }
</script>


<style scoped lang='scss'>

  @mixin font {
    font-family: SourceSansPro-Regular;
    font-size: .14rem;
    color: #354052;
    line-height: .21rem;
  }

  .search-input {
    margin-top: .46rem;
    padding-left: .2rem;
    position: relative;
    height: .36rem;
    overflow: hidden;
    input {
      @include font;
      padding: 0 .34rem 0 .12rem;
      width: 100%;
      line-height: .34rem;
      border: .01rem solid #DFE3E9;
      border-radius: .04rem;
      background-color: #fff;
    }
    i {
      position: absolute;
      right: .11rem;
      top: 50%;
      transform: translateY(-50%);
      font-size: .14rem;
      color: #1991EB;
    }
  }
</style>
