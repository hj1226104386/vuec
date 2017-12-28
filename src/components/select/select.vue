<template>
  <div class="select-wrapper" :class='{blueBorder:isShowSelect}' @click.stop='expandSelect'>
    <i class='iconfont icon-sanjiao fr' :class='{"arrow-rotate":isShowSelect}'></i>
    <!--下拉框默认值-->
    <span>{{selectedContent}}</span>
    <ul class="select" v-show='isShowSelect'>
      <li v-for='(one,index) in options' :class='{activeOption:tempInd===index}'
          @click='activeOption(index,one.name,one.value)'>
        {{one.name}}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'v-select',
    props: ['options', 'defaultText', 'value'],
    data () {
      return {
        tempInd: '', // 用于动态切换样式
        isShowSelect: false, // 是否显示下拉框
        selectedContent: this.defaultText
      }
    },
    methods: {
      // 展开/收起下拉框
      expandSelect: function () {
        this.isShowSelect = !this.isShowSelect
      },
      activeOption: function (index, text, value) {
        this.tempInd = index
        // 向父组件传选中的值
        this.selectedContent = text
        this.$emit('update:value', value)
      }
    }
  }
</script>


<style scoped lang='scss'>
  // 下拉框option选中时的样式
  .activeOption {
    color: #2EA2F8 !important;
    background-color: #F1F4F8;
  }

  // 下拉框点击蓝色边框样式
  .blueBorder {
    border-color: #2EA2F8 !important;
  }

  // 箭头旋转
  .arrow-rotate {
    transform: rotate(180deg);
  }

  @mixin border($borderColor) {
    border: 1px solid $borderColor;
    border-radius: 4px;
  }

  @mixin selectFont {
    font-family: SourceSansPro-Regular;
    font-size: 14px;
    color: #354052;
    line-height: 21px;
  }

  .select-wrapper {
    display: inline-block;
    padding: 0 16px;
    position: relative;
    width: 100px;
    height: 36px;
    font-family: SourceSansPro-Regular;
    cursor: pointer;
    background-color: #F6F7F9;
    vertical-align: middle;
    transition: border .3s ease-in-out;
    @include border(#DFE3E9);
    span {
      display: block;
      padding-right: 10px;
      line-height: 36px;
      height: 100%;
      font-size: 14px;
      text-align: left !important;
      color: #354052;
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    i {
      margin-top: 11px;
      height: 12px;
      line-height: 12px;
      font-size: .12px;
      transition: all .3s linear;
      transform-origin: center center;
    }
  }

  /*公共下拉框样式*/
  .select {
    position: absolute;
    padding: 0;
    left: 0;
    top: 36px;
    z-index: 198;
    width: 100%;
    border: 1px solid #C5D0DE;
    border-bottom: none;
    border-top: none;
    background-color: #fff;
    overflow: hidden;
    li {
      @include selectFont;
      padding: 0 13px;
      margin: 0 !important;
      width: 100%;
      height: 36px;
      line-height: 36px;
      border-bottom: 1px solid #C5D0DE;
    }
  }

</style>
