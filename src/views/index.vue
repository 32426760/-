<template>
  <div class="index">
    <el-container>
      <el-header style="border-bottom:1px solid #eee;">
        <el-menu
          :router="true"
          :default-active="activeIndex"
          class="el-menu-demo w"
          mode="horizontal"
        >
          <el-menu-item>
            <div class="logo">
              <img src="../assets/logo.jpg" alt />
              <div class="logoName">衣家 YIJIA</div>
            </div>
          </el-menu-item>
          <el-submenu index="1" style="width:100px;overflow:hidden">
            <template slot="title">研发部</template>
            <el-menu-item index="/itemDesign">设计项目</el-menu-item>
            <el-menu-item index="/materialPurchase">版料采购</el-menu-item>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">板房</template>
            <el-menu-item index="/pattern">纸样</el-menu-item>
            <el-menu-item index="/platemaking">制版</el-menu-item>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title">销售</template>
            <el-menu-item index="/clientManagement">客户管理</el-menu-item>
            <el-menu-item index="3-2">销售订单</el-menu-item>
          </el-submenu>
          <el-submenu index="4">
            <template slot="title">生产</template>
            <el-menu-item index="/productionOrders">生产下单</el-menu-item>
            <el-menu-item index="/purchase">采购</el-menu-item>
            <el-menu-item index="/productionScheduling">生产排期</el-menu-item>
          </el-submenu>
          <el-submenu index="5">
            <template slot="title">仓库</template>
            <el-menu-item index="/stockInquiry">仓库查询</el-menu-item>
            <el-menu-item index="/productStorehouse">仓品回仓</el-menu-item>
          </el-submenu>
          <el-submenu index="6">
            <template slot="title">档案库</template>
            <el-menu-item index="/distributor">供应商</el-menu-item>
            <el-menu-item index="/routeCard">物料工艺卡</el-menu-item>
            <el-menu-item index="6-3">款式档案</el-menu-item>
          </el-submenu>
          <el-submenu index="7">
            <template slot="title">财务</template>
            <el-menu-item index="/paymentReimbursement">预支报销</el-menu-item>
            <!-- <el-menu-item index="7-2">财务统计</el-menu-item> -->
            <el-menu-item index="/accountFlowAndBookkeeping">账户流水及记账</el-menu-item>
            <el-menu-item index="/customerReconciliationAndCollection">客户对账及收款</el-menu-item>
            <el-menu-item index="/supplierReconciliationAndPayment">供应商对账及付款</el-menu-item>
            <el-menu-item index="/accounter">帐户管理</el-menu-item>
            <el-menu-item index="/accountType">账目类型</el-menu-item>
          </el-submenu>
          <el-submenu index="8">
            <template slot="title">设置</template>
            <el-menu-item index="/goodsCategory">商品分类</el-menu-item>
            <el-menu-item index="/colorManagement">颜色管理</el-menu-item>
            <el-menu-item index="/measurementManagement">尺码管理</el-menu-item>
            <el-menu-item index="/materialManagement">材质管理</el-menu-item>
            <el-menu-item index="/timeManagement">季节管理</el-menu-item>
            <el-menu-item index="/unitManagement">单位管理</el-menu-item>
          </el-submenu>
        </el-menu>
      </el-header>
      <el-main>
        <router-view class="w"></router-view>
      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeIndex: "2"
    };
  }
};
</script>

<style lang="less" scoped>
.index {
  .logo {
    display: flex;
    justify-content: center;
    align-items: center;
    img {
      width: 40px;
      height: 40px;
      margin-right: 10px;
    }
    .logoName {
      font-size: 20px;
      color: #000;
    }
  }
  // /deep/.el-submenu__title{
  //   width: 120px;
  // }
}
</style>