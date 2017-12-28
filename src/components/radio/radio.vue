<template>
  <div class="radio-wrapper">
    <div class="radio-item" v-for='(one,index) in radioItems'>
      <input :id="'Radio'+one.id" type="radio" name='radioItem' :value='one.value' v-model='radioValue'>
      <label :for="'Radio'+one.id">
        <span class='wenli'>{{one.name}}</span>
      </label>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'radio',
    props: ['radioItems'],
    data () {
      return {
        radioValue: this.radioItems[0].value
      }
    },
    mounted: function () {
      // 默认先返回默认值
      this.$emit('radioValueFromRadio', this.radioValue)
    },
    // 监听单选框的变化
    watch: {
      radioValue: function (newV, oldV) {
        // 自定义事件，向父组件传递最新选中的radio的value值
        this.$emit('radioValueFromRadio', newV)
      }
    }
  }
</script>


<style scoped>
  .radio-wrapper > .radio-item {
    display: inline-block;
    height: .22rem;
  }

  .radio-item > input {
    display: none;
  }

  .radio-item > label {
    display: inline-block;
    position: relative;
    margin-right: .2rem;
  }

  .radio-item > input + label:before {
    content: '';
    position: absolute;
    left: 0;
    top: .03rem;
    width: .16rem;
    height: .16rem;
    border-radius: 50%;
    border: .01rem solid rgba(0, 0, 0, .2);
  }

  .radio-item > input:checked + label::before {
    border: none;
    background-color: #327FFF;
  }

  .radio-item > input:checked + label::after {
    content: '';
    position: absolute;
    left: .05rem;
    top: 50%;
    width: .06rem;
    height: .06rem;
    transform: translateY(-50%);
    background-color: #fff;
    border-radius: 50%;
  }

  .radio-item > label > span {
    display: inline-block;
    margin-left: .28rem;
    font-family: SourceSansPro-Regular;
    font-size: .14rem;
    color: #354052;
    line-height: .22rem;
  }
</style>
