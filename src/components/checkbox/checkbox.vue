<template>
  <div class="check-box">
    <span class='checkbox-item' v-for='(one,index) in checkboxItems'>
      <input class='check-box-input' type="checkbox" :id="'Checkbox'+(random+index)" :value="one.value"
             v-model='checkboxValue'>
      <label :for="'Checkbox'+(random+index)"></label>
      <span>{{one.name}}</span>
    </span>
  </div>
</template>

<script>
  export default {
    name: 'checkBox',
    props: ['checkboxItems', 'value'],
    data () {
      return {
        random: Math.floor((Math.random()) * 1000),
        checkboxValue: []
      }
    },
    watch: {
      checkboxValue: {
        handler: function (valueArr) {
          this.$emit('update:value', valueArr)
        },
        deep: true
      }
    }
  }
</script>


<style scoped lang='scss'>
  .check-box {
    display: inline-block;
    span {
      line-height: 21px;
      width: auto !important;
      label {
        display: inline-block;
        margin-right: 10px;
        margin-left: 0;
        vertical-align: sub;
        transition: background-color .2s ease;
      }
      .check-box-input + label {
        position: relative;
        margin-right: 10px;
        margin-left: 0;
        width: 16px;
        height: 16px;
        border-radius: 4px;
        border: 1px solid #DFE3E9;
      }
      .check-box-input:checked + label {
        margin-right: 10px;
        margin-left: 0;
        width: 16px;
        height: 16px;
        border-radius: 4px;
        border: 1px solid #007AFF;
        background-color: #007AFF;
      }
      .check-box-input:checked + label:after {
        content: '✔';
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: #fff;
      }
      span {
        display: inline-block;
        margin-right: 20px;
        font-family: SourceSansPro-Regular;
        font-size: 14px;
        color: #354052;
        line-height: 21px;
      }
    }
  }
</style>
