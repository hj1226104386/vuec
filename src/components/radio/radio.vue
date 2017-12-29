<template>
  <div class="radio-wrapper">
    <div class="radio-item" v-for='(one,index) in radioItems'>
      <input :id="'Radio'+(random+index)" type="radio" name='radioItem' :value='one.value' v-model='radioValue'>
      <label :for="'Radio'+(random+index)">
        <span class='wenli'>{{one.name}}</span>
      </label>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'radio',
    props: ['radioItems', 'value'],
    data () {
      return {
        random: Math.floor((Math.random()) * 1000),
        radioValue: this.radioItems[0].value
      }
    },
    mounted: function () {
      // 默认先返回默认值
      this.$emit('update:value', this.radioValue)
    },
    // 监听单选框的变化
    watch: {
      radioValue: function (newV, oldV) {
        // 自定义事件，向父组件传递最新选中的radio的value值
        this.$emit('update:value', newV)
      }
    }
  }
</script>


<style scoped>
  .radio-wrapper > .radio-item {
    display: inline-block;
    height: 22px;
  }

  .radio-item > input {
    display: none;
  }

  .radio-item > label {
    display: inline-block;
    position: relative;
    margin-right: 20px;
    cursor: pointer;
  }

  .radio-item > input + label:before {
    content: '';
    position: absolute;
    left: 0;
    top: 3px;
    width: 16px;
    height: 16px;
    border-radius: 50%;
    border: 1px solid rgba(0, 0, 0, .2);
  }

  .radio-item > input:checked + label::before {
    border: none;
    background-color: #327FFF;
  }

  .radio-item > input:checked + label::after {
    content: '';
    position: absolute;
    left: 4px;
    top: 50%;
    width: 8px;
    height: 8px;
    transform: translateY(-50%);
    transform-origin: center center;
    background-color: #fff;
    border-radius: 50%;
  }

  .radio-item > label > span {
    display: inline-block;
    margin-left: 28px;
    font-family: SourceSansPro-Regular;
    font-size: 14px;
    color: #354052;
    line-height: 22px;
  }
</style>
