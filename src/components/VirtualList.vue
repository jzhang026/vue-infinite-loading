<template>
  <div class="root">
    <div class="scroll" ref="scroll" @scroll="onScroll">
      <div class="container" :style="{ height: `${totalCount * itemHeight}px` }">
        <table :style="{ transform: `translateY(${beforeCount * itemHeight}px)`}">
          <tbody>
            <tr v-for="data in showDataSource" v-bind:key="data.name">
              <td>{{data.index}}</td>
              <td>{{data.name}}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import { faker } from '@faker-js/faker'

/*
 * @param scrollTop 滚动的高度
 * @param pageSize 每页的行数
 * @param itemHeight 每行的高度
 */
function getPageNum({ scrollTop, pageSize, itemHeight }) {
  const pageHeight = pageSize * itemHeight
  return Math.max(Math.floor(scrollTop / pageHeight), 1)
}

/*
 * @param pageNum 当前的页码
 * @param pageSize 每页的行数
 * @param dataSource 总数据
 */
function getShowData({ pageNum, pageSize, dataSource }) {
  const startIndex = (pageNum - 1) * pageSize
  const endIndex = Math.min((pageNum + 2) * pageSize, dataSource.length)

  console.log(startIndex, endIndex)
  return {
    showDataSource: dataSource.slice(startIndex, endIndex),
    beforeCount: startIndex,
    afterCount: dataSource.length - endIndex,
    totalCount: dataSource.length,
  }
}

export default {
  name: 'App',
  data() {
    return {
      // 数据总条数
      totalCount: 0,
      // 前置条数
      beforeCount: 0,
      // 每行的总高度
      itemHeight: 24,
      // 当前的分页数，默认1
      pageNum: 1,
      // 每页的条数
      pageSize: 20,
      // 总的数据
      dataSource: [],
      // 显示的数据
      showDataSource: [],
    }
  },

  mounted() {
    this.createDataSource()
    this.setShowDataSource()
  },

  methods: {
    // 创建数据, 模拟10000条数据
    createDataSource() {
      this.dataSource = Array.from({ length: 10000 }).map((item, index) => ({
        index,
        name: faker.lorem.lines(1),
      }))
    },
    getMaxPageNum() {
      return getPageNum({
        scrollTop: this.$refs.scroll.scrollHeight - this.$refs.scroll.clientHeight,
        pageSize: this.pageSize,
        itemHeight: this.itemHeight,
      })
    },
    setPageNum() {
      const maxPageNum = this.getMaxPageNum()
      const pageNum = getPageNum({
        scrollTop: this.$refs.scroll.scrollTop,
        pageSize: this.pageSize,
        itemHeight: this.itemHeight,
      })

      const currPageNum = Math.min(pageNum, maxPageNum)
      // 检测页码与上一次是否改变
      if (currPageNum === this.pageNum) return false

      this.pageNum = currPageNum
      return true
    },
    setShowDataSource() {
      const { showDataSource, beforeCount, totalCount } = getShowData({
        pageNum: this.pageNum,
        pageSize: this.pageSize,
        dataSource: this.dataSource,
      })

      this.showDataSource = showDataSource
      this.beforeCount = beforeCount
      this.totalCount = totalCount
    },

    onScroll() {
      const isUpdated = this.setPageNum()
      if (!isUpdated) return

      this.setShowDataSource()
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  margin: 0;
}
.root {
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 24px;
  background: #ccc;
  height: 100vh;
  box-sizing: border-box;
}
table {
  width: 100%;
}

table tr:nth-child(odd) {
  background: #fafafa;
}

table tr td {
  height: 24px;
  padding: 0;
}

.scroll {
  height: 480px;
  width: 480px;
  overflow: auto;
  background: #fff;
}
</style>
