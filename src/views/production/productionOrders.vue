<template>
  <div class="productionOrders">
    <!-- 面包屑 -->
    <el-breadcrumb separator="/" class="breadcrumb">
      <img src="../../assets/mbxlogo.svg" alt class="mbxlogo" />
      <el-breadcrumb-item>生产</el-breadcrumb-item>
      <el-breadcrumb-item>生产下单</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="main">
      <el-form :inline="true" :model="formInline" class="demo-form-inline">
        <el-form-item label="商品">
          <el-input v-model="formInline.user" placeholder="审批人"></el-input>
        </el-form-item>
        <el-form-item label="年份">
          <el-select v-model="year" placeholder="年份" style="width:120px">
            <el-option v-for="item in years" :key="item.id" :label="item.year" :value="item.year"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="季节">
          <el-select v-model="season" placeholder="季节" style="width:120px">
            <el-option
              v-for="item in seasons"
              :key="item.id"
              :label="item.season"
              :value="item.season"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="设计师">
          <el-select
            v-model="stylist"
            placeholder="设计师"
            @change="handleUser_id($event)"
            style="width:120px"
          >
            <el-option v-for="item in stylists" :key="item.id" :label="item.name" :value="item.id"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="类别">
          <el-select v-model="category" placeholder="类别" style="width:120px">
            <el-option
              v-for="item in categorys"
              :key="item.id"
              :label="item.style_type"
              :value="item.style_type"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="客户">
          <el-select
            v-model="west"
            placeholder="西所"
            @change="handleCustomer_id($event)"
            style="width:120px"
          >
            <el-option
              v-for="item in wests"
              :key="item.id"
              :label="item.companyname"
              :value="item.id"
            ></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="状态">
          <el-select
            v-model="state"
            placeholder="状态"
            @change="handelState($event)"
            style="width:120px"
          >
            <el-option v-for="item in states" :key="item.id" :label="item.v" :value="item.id"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item>
          <el-button @click="onSubmit">查询</el-button>
        </el-form-item>
      </el-form>
      <div class="table">
        <el-table ref="singleTable" :data="tableData" highlight-current-row style="width: 100%">
          <el-table-column type="index" width="50"></el-table-column>
          <el-table-column label="图片">
            <template slot-scope="scope">
              <img :src="scope.row.picimg" class="img" alt />
            </template>
          </el-table-column>
          <el-table-column property="username" label="名称"></el-table-column>
          <el-table-column property="stylenumber" label="款号"></el-table-column>
          <el-table-column property="color" label="颜色"></el-table-column>
          <el-table-column property="category" label="品类"></el-table-column>
          <el-table-column property="year" label="年份"></el-table-column>
          <el-table-column property="season" label="季节"></el-table-column>
          <el-table-column property="stylist" label="设计师"></el-table-column>
          <el-table-column property="west" label="客户"></el-table-column>
          <el-table-column property="number" label="数量"></el-table-column>
          <el-table-column property="state" label="状态"></el-table-column>

          <el-table-column label="操作">
            <template slot-scope="scope">
              <el-button
                class="elbtn"
                size="mini"
                @click="handleEdit(scope.$index, scope.row)"
              >{{scope.row.operation}}</el-button>
            </template>
          </el-table-column>
        </el-table>
      </div>
    </div>
    <div style="display: flex;justify-content: space-between;align-items: center;">
      <!-- 打印  导出-->
      <div class="btn">
        <el-button size="mini">打印</el-button>
        <el-button size="mini">导出</el-button>
      </div>
      <!-- 分页 -->
      <el-pagination
        class="pagination"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="pageIndex"
        :page-sizes="[10, 20, 30, 40]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
      ></el-pagination>
    </div>
  </div>
</template>

<script>
import {
  getYearList,
  getSeasonList,
  getStylistList,
  getCategoryList,
  getWestList
} from "@/api/researchDevelopment";
export default {
  data() {
    return {
      formInline: {
        user: "",
        region: ""
      },
      years: [],
      seasons: [],
      stylists: [],
      categorys: [],
      wests: [],
      pageIndex: 1,
      pageSize: 10,
      total: 0,
      year: "", //年
      season: "", //季节
      stylist: "", //设计师
      category: "", //类别
      west: "", //西所
      state: "", //状态
      states: [
        {
          v: "未下单",
          id: 0
        },
        {
          v: "已下单",
          id: 1
        }
      ],
      tableData: [
        {
          picimg:
            "https://axure-file.lanhuapp.com/b0e7ed9c-a55b-4903-972b-002bbf42cf81__9baf896cacfe3438e33a5434b694f14c.svg",
          username: "aa",
          stylenumber: "aa",
          color: "aa",
          category: "aa",
          year: "aa",
          season: "aa",
          stylist: "aa",
          west: "aa",
          number: "aa",
          state: "aa",
          operation: "aa"
        }
      ]
    };
  },
  methods: {
    handleEdit() {
      this.$router.push({ path: "/designFile" });
    },
    onSubmit() {
      console.log("submit!");
    }, // 获取customer_id
    handleCustomer_id(e) {
      this.customer_id = e;
    },
    // state
    handelState(e) {
      this.stateId = e;
    },
    async getYear() {
      let res = await getYearList();
      let { data } = res.data;
      console.log(data);
      this.years = data;
    },
    async getSeason() {
      let res = await getSeasonList();
      let { data } = res.data;
      console.log(data);
      this.seasons = data;
    },
    async getStylist() {
      let res = await getStylistList();
      let { data } = res.data;
      console.log(data);
      this.stylists = data;
    },
    async getCategory() {
      let res = await getCategoryList();
      let { data } = res.data;
      console.log(data);
      this.categorys = data;
    },
    async getWest() {
      let res = await getWestList();
      let { data } = res.data;
      console.log(data);
      this.wests = data;
    },
    handleSizeChange(val) {
      this.pageSize = val;
    },
    handleCurrentChange(val) {
      this.pageIndex = val;
    }
  },
  mounted() {
    this.getYear();
    this.getSeason();
    this.getStylist();
    this.getCategory();
    this.getWest();
  }
};
</script>

<style lang="less" scoped>
.productionOrders {
  .main {
    margin: 20px;
    .table {
      .img {
        width: 40px;
        height: 40px;
      }
    }
  }
}
</style>