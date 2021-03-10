<template>
    <div>
      <h2>测试页面 {{ msg }}</h2>
      <el-table
        :data="tableData"
        style="width: 100%">
        <el-table-column
          prop="id"
          label="ID"
          width="180">
        </el-table-column>
        <el-table-column
          prop="username"
          label="姓名"
          width="180">
        </el-table-column>
        <el-table-column
          prop="password"
          label="地址">
        </el-table-column>
      </el-table>
    </div>
</template>

<script>
import { testInfo, pay, getAllAdmin } from '@/api/test'
export default {
  name: 'TextIndex',
  data() {
    return {
      msg: '',
      tableData: []
    }
  },
  mounted() {
    this.getAdmin()
  },
  methods: {
    getAdmin() {
      getAllAdmin().then(res => {
        this.tableData = res.data
      })
    },
    getInfo() {
      testInfo().then(res => {
        this.msg = res.data
      })
    },
    payTest() {
      pay().then(res => {
        document.querySelector('body').innerHTML = res // 查找到当前页面的body，将后台返回的form替换掉他的内容
        document.forms[0].submit() // 执行submit表单提交，让页面重定向，跳转到支付宝页面
      })
    }
  }
}
</script>

<style scoped>

</style>
