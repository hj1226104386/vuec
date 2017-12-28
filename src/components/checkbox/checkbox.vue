<template>
  <div class="check-box">
    <span class='checkbox-item' v-for='(one,index) in checkboxItems'>
      <input class='check-box-input' type="checkbox" :id="'Checkbox'+one.id" :value="one.value"
             v-model='checkboxValue' @click='broadcast'>
      <label :for="'Checkbox'+one.id"></label>
      <span>{{one.name}}</span>
    </span>
  </div>
</template>

<script>
  export default {
    name: 'checkBox',
    props: ['checkboxItems'],
    data () {
      return {
        checkboxValue: []
      }
    },
    mounted: function () {},
    methods: {
      // 将选中的选项传给父组件
      broadcast: function () {
        var that = this
        // TODO:异步获取，不然不能立马获取选中的选择的value
        setTimeout(function () {
          that.$emit('valueArrFromCheckbox', that.checkboxValue)
        }, 10)
      }
    }
  }
</script>


<style scoped lang='scss'>
  .check-box {
    display: inline-block;
    span {
      line-height: .21rem;
      width: auto !important;
      label {
        display: inline-block;
        margin-right: .1rem;
        margin-left: 0;
        vertical-align: sub;
        transition: background-color .2s ease;
      }
      .check-box-input + label {
        margin-right: .1rem;
        margin-left: 0;
        width: .16rem;
        height: .16rem;
        border-radius: .04rem;
        border: .01rem solid #DFE3E9;
      }
      .check-box-input:checked + label {
        margin-right: .1rem;
        margin-left: 0;
        width: .16rem;
        height: .16rem;
        border-radius: .04rem;
        border: .01rem solid #007AFF;
        background-color: #007AFF;
      }
      .check-box-input:checked + label {
        width: .16rem;
        height: .16rem;
        border-radius: .04rem;
        border: .01rem solid #DFE3E9;
      }
      span {
        display: inline-block;
        margin-right: .2rem;
        font-family: SourceSansPro-Regular;
        font-size: .14rem;
        color: #354052;
        line-height: .21rem;
      }
    }
  }
</style>
