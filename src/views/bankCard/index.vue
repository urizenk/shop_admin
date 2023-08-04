<template>
  <div class="bank-card">
    <el-card>
      <div slot="header" class="clearfix">
        <span>银行卡管理</span>
        <el-button type="primary" class="fr" size="mini" icon="Plus">
          添加银行卡
        </el-button>
      </div>
      <el-table :data="cardList" border align="center" style="width: 100%">
        <el-table-column
          label="序号"
          width="100"
          align="center"
          type="index"
        ></el-table-column>
        <el-table-column
          prop="name"
          label="姓名"
          width="100"
          align="center"
        ></el-table-column>
        <el-table-column
          prop="bankName"
          label="开户行名称"
          width="280"
          align="center"
        ></el-table-column>
        <el-table-column
          prop="bankCard"
          label="卡号"
          align="center"
        ></el-table-column>
      </el-table>
    </el-card>
    <!-- 写一个分页器 -->
    <el-pagination
      v-model:page-size="pageSize"
      v-model:current-page="currentPage"
      :page-sizes="[3, 5, 7, 9]"
      hide-on-single-page
      background
      layout="prev, pager, next, jumper, ->,sizes ,total"
      :total="100"
    />
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, toRefs, onMounted } from 'vue'
import { reqBankCardInfo } from '@/api/bankcard/index'

let cardList = ref([])

onMounted(async () => {
  const res = await reqBankCardInfo()
  cardList.value = res.data.records
})
</script>
<style scoped lang="scss">
.bank-card {
  .clearfix {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .el-card__header {
    padding: 0 20px;
  }
  .el-pagination {
    position: absolute;
    bottom: 30px;
    justify-content: space-around;
  }
}
</style>
