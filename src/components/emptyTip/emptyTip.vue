<template>
  <div class="empty-tip-wrapper">
    <div class="empty-tip">
      <i class='iconfont icon-search'></i>
      <p>
        <slot>
          没有传入内容时默认显示的内容
        </slot>
      </p>
    </div>
  </div>
</template>

<script>

</script>


<style scoped>
.empty-tip-wrapper{
  position: relative;
  width: 100%;
  min-height:4rem;
}
  .empty-tip{
    position: absolute;
    top:53%;
    left:50%;
    transform:translateX(-50%);
    text-align: center;
    color:#3399ff;
  }
.empty-tip>i{
  font-size:.3rem;
}
.empty-tip>p{
  margin-top: .1rem;
  font-size:.14rem;
}
</style>
