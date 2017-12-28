<template>
  <div class="hello">
    <h1>组件测试</h1>
    <!--loading组件-->
    <!--<Loading>加载吧，骚年</Loading>-->

    <!--下拉框组件-->
    <v-select :options='selectOptions' default-text='快选择' :value.sync='selectValue'></v-select>
  </div>
</template>

<script>
  import Loading from './loading/loading'
  import select from './select/select'

  export default {
    name: 'HelloWorld',
    components: {
      Loading,
      'v-select': select
    },
    data () {
      return {
        // 下拉框
        selectOptions: [{name: '选项1', value: 0}, {name: '选项2', value: 1}],
        selectValue: ''
      }
    },
    watch: {
      selectValue: function (a, b) {
        console.log(a)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hello > h1 {
    padding-bottom: 20px;
    border-bottom: 3px solid orange;
  }
</style>
