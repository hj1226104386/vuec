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
    <!--loading-->
    <v-loading v-show='ifShowLoading'></v-loading>
  </div>
</template>

<script>
  export default {
    name: 'paginator',
    props: ['ajaxData', 'pageSize', 'totalPages'],
    data () {
      return {
        currentPage: 1,
        showItem: 7,
        totalPage: 1, // ajax获取
        ifShowLoading: false
      }
    },
    watch: {
      // 监控从父组件传来的搜索参数和请求接口
      ajaxData: {
        handler: function (newV, oldV) {
//          console.log('参数变动了')
          // 默认还是第一页
          this.currentPage = 1
          this.ajax(newV)
        },
        deep: true
      },
      // 监听从父组件传来的总页数，这是默认的，后面需要通过ajax去请求来获取 -师资列表
      totalPages: function () {
        this.totalPage = this.totalPages || 1
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
    },
    methods: {
      goto: function (index) {
        if (index === this.currentPage) return false
        this.currentPage = index
        // TODO:这里发送ajax请求
        this.ajax(this.ajaxData)
      },
      ajax: function (data) {
        var that = this
        // 显示loading
//        that.ifShowLoading = true
        var url = data.ajaxUrl
        var params = data.params
        var otherParams = this.$common.calcParams()
        var pageParams = {page: this.currentPage, pageSize: this.pageSize}
        var totalParams = Object.assign(otherParams, params, pageParams)
        this.$http.post(url, totalParams, {emulateJSON: true}).then(function (res) {
          // 保存查询到的表格数据
          that.$store.commit('setTableData', res.body.data || [])
          that.totalPage = res.body.totalPage
//          that.ifShowLoading = false
        })
      }
    }
  }
</script>


<style scoped lang='scss'>
  .paginator {
    padding: .29rem 0 .27rem;
    text-align: center;
  }

  .pagination {
    position: relative;
    li {
      display: inline-block;
      margin: 0 .071rem;
      line-height: .34rem;
      width: .34rem;
      height: .34rem;
      border: .01rem solid #E4E4E4;
      background-color: rgba(32, 53, 128, 0.01);
      a {
        display: inline-block;
        font-family: PingFangSC-Regular;
        font-size: .14rem;
        color: #354052;
        letter-spacing: 0;
        line-height: .21rem;
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
        width: .54rem;
        height: .34rem;
      }
      &.page-turning {
        width: .85rem;
        height: .34rem;
      }
    }
  }
</style>
