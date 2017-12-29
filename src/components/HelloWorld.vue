<template>
  <div class="hello">
    <h1>组件测试</h1>
    <!--loading组件-->
    <!--<Loading>加载吧，骚年</Loading>-->

    <!--下拉框组件-->
    <!--<v-select :options='options' default-text='快选择' :value.sync='selectValue'></v-select>-->

    <!--单选框组件-->
    <!--<v-radio :radio-items='options' :value.sync='radioValue'></v-radio>-->

    <!--多选框组件-->
    <!--<v-checkbox :checkbox-items='options' :value.sync='checkboxValue'></v-checkbox>-->

    <!--分页组件-->
    <v-paginator :page-size='10' :total-page='3' test></v-paginator>
  </div>
</template>

<script>
  import Loading from './loading/loading'
  import select from './select/select'
  import radio from './radio/radio.vue'
  import checkbox from './checkbox/checkbox.vue'
  import paginator from './paginator/paginator.vue'

  export default {
    name: 'HelloWorld',
    components: {
      Loading,
      'v-select': select,
      'v-radio': radio,
      'v-checkbox': checkbox,
      'v-paginator': paginator
    },
    data () {
      return {
        // 下拉框
        options: [{name: '选项1', value: 1}, {name: '选项2', value: 2}],
        selectValue: '',
        radioValue: '',
        checkboxValue: ''
      }
    },
    watch: {
      selectValue: function (a, b) {
        console.log(a)
      },
      radioValue: function (a, b) {
        console.log(a)
      },
      checkboxValue: function (a, b) {
        console.log(a)
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .hello > h1 {
    margin-bottom: 20px;
    padding-bottom: 20px;
    font-size: 20px;
    border-bottom: 3px solid orange;
  }
</style>
