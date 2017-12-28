<template>
  <div class="loading">
    <p>
      <slot>拼命加载中...</slot>
    </p>
    <img src="./loading.gif">
  </div>
</template>

<script>

</script>


<style scoped>
  /*loading样式*/
  .loading {
    position: fixed;
    top: 46%;
    left: 50%;
    z-index: 999;
    width: 130px;
    height: 100px;
    transform: translateX(-50%);
    text-align: center;
    border-radius: 6px;
    background-color: rgba(0, 0, 0, .5);
  }

  .loading > p {
    margin: 15px 0 15px;
    color: #fff;
    font-size: 16px;
  }

  .loading > img {
    width: 40px;
    height: 40px;
  }

</style>
