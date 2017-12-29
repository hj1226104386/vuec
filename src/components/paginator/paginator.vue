<template>
  <div class='paginator' v-show='totalPage>0'>
    <ul class="pagination">
      <li class='edge-page' @click="goto(1)"><a href="javascript:;">首页</a></li>
      <li class='page-turning' v-show="currentPage != 1" @click="currentPage-- && goto(currentPage--)"><a
        href="javascript:;">上一页</a>
      </li>
      <li v-for="index in pages" @click="goto(index)" :class="{'active':currentPage == index}" :key="index">
        <a href="javascript:;">{{index}}</a>
      </li>
      <li class='page-turning' v-show="totalPage != currentPage&&totalPage!==1 && totalPage != 0 "
          @click="currentPage++ && goto(currentPage++)"><a href="javascript:;">下一页</a></li>
      <li class='edge-page' @click="goto(totalPage)"><a href="javascript:;">尾页</a></li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'paginator',
    props: ['pageSize', 'totalPage', 'test'],
    data () {
      return {
        currentPage: 1,
        showItem: 7
      }
    },
    mounted: function () {
      console.log(this.test)
    },
    methods: {
      goto: function (index) {
        if (index === this.currentPage) return false
        this.currentPage = index
      }
    },
    computed: {
      pages: function () {
        var pageArr = []
        var i
        if (this.currentPage < this.showItem) { // 如果当前的激活的项 小于要显示的条数
          // 总页数和要显示的条数那个大就显示多少条
          i = Math.min(this.showItem, this.totalPage)
          while (i) {
            pageArr.unshift(i--)
          }
        } else { // 当前页数大于显示页数了
          var middle = this.currentPage - Math.floor(this.showItem / 2) // 从哪里开始
          i = this.showItem
          if (middle > (this.totalPage - this.showItem)) {
            middle = (this.totalPage - this.showItem) + 1
          }
          while (i--) {
            pageArr.push(middle++)
          }
        }
        return pageArr
      }
    }
  }
</script>


<style scoped lang='scss'>
  .paginator {
    text-align: center;
  }

  .pagination {
    position: relative;
    li {
      display: inline-block;
      margin: 0 7px;
      line-height: 34px;
      width: 34px;
      height: 34px;
      border: 1px solid #E4E4E4;
      background-color: rgba(32, 53, 128, 0.01);
      a {
        display: inline-block;
        font-family: PingFangSC-Regular;
        font-size: 14px;
        color: #354052;
        letter-spacing: 0;
        line-height: 21px;
        background-color: rgba(32, 53, 128, 0.01);
      }
      &.active {
        color: #fff;
        border: none;
        background-color: #1991EB;
        & {
          a {
            color: #fff;
          }
        }
      }
      &.edge-page {
        width: 54px;
        height: 34px;
      }
      &.page-turning {
        width: 85px;
        height: 34px;
      }
    }
  }
</style>
