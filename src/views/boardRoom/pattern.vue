<template>
  <div class="pattern">
    <!-- 面包屑 -->
    <el-breadcrumb separator="/" class="breadcrumb">
      <img src="../../assets/mbxlogo.svg" alt class="mbxlogo" />
      <el-breadcrumb-item>板房</el-breadcrumb-item>
      <el-breadcrumb-item>纸样</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="main">
      <!-- search_condition -->
      <div class="search_condition">
        <el-form :inline="true" :model="formInline" class="demo-form-inline">
          <el-form-item label="款式">
            <el-input v-model="formInline.name" placeholder="名称、款号"></el-input>
          </el-form-item>
          <span @click.capture="getStylist">
            <el-form-item label="设计师">
              <el-select
                v-model="formInline.stylist"
                placeholder="设计师"
                @change="handleUser_id($event)"
              >
                <el-option
                  v-for="item in stylists"
                  :key="item.id"
                  :label="item.name"
                  :value="item.id"
                ></el-option>
              </el-select>
            </el-form-item>
          </span>
          <span @click.capture="getCategory">
            <el-form-item label="状态">
              <el-select v-model="formInline.category" placeholder="类别">
                <el-option
                  v-for="item in categorys"
                  :key="item.id"
                  :label="item.style_type"
                  :value="item.style_type"
                ></el-option>
              </el-select>
            </el-form-item>
          </span>
          <el-form-item>
            <div @click="handleInquire" class="inquire">查询</div>
          </el-form-item>
        </el-form>
      </div>
      <div class="table">
        <el-table ref="singleTable" :data="tableData" highlight-current-row style="width: 100%">
          <el-table-column type="index" width="50"></el-table-column>
          <el-table-column label="图片" width="60">
            <template slot-scope="scope">
              <img :src="scope.row.picimg" class="img" alt />
            </template>
          </el-table-column>
          <el-table-column property="colorimg">
            <template slot-scope="scope">
              <img :src="scope.row.colorimg" class="img" alt />
            </template>
          </el-table-column>
          <el-table-column property="color" label="颜色"></el-table-column>
          <el-table-column property="username" label="名称"></el-table-column>
          <el-table-column property="stylenumber" label="款号"></el-table-column>
          <el-table-column property="category" label="品类"></el-table-column>
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
  </div>
</template>

<script>
import {
  getStylistList,
  getCategoryList
  // getCategoryList
} from "@/api/researchDevelopment";
export default {
  data() {
    return {
      formInline: {
        name: "",
        category: "",
        stylist: ""
      },
      pageIndex: 1,
      pageSize: 10,
      total: 0,
      user_id: "",
      tableData: [
        {
          picimg:
            "https://axure-file.lanhuapp.com/b0e7ed9c-a55b-4903-972b-002bbf42cf81__9baf896cacfe3438e33a5434b694f14c.svg",
          colorimg: "http://localhost:8080/img/logo.2c53d74c.jpg",
          color: "王小虎",
          username: "王小虎",
          stylenumber: "王小虎",
          category: "王小虎",
          state: "王小虎",
          operation: "王小虎",
          id: 40
        }
      ],
      categorys: [],
      stylists: [],
      categorys: []
    };
  },
  methods: {
    handleInquire() {
      console.log(this.formInline);
    },
    handleEdit(index, row) {
      console.log(index, row);
      this.$router.push({ path: `/patternStatus?id=${row.id}` });
    },
    handleUser_id(e) {
      this.user_id = e;
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
    }
  }
};
</script>
<style lang="less" scoped>
.pattern {
  .main {
    margin: 20px;
    .search_condition {
      .inquire {
        width: 100px;
        height: 40px;
        background-color: #000;
        display: flex;
        justify-content: center;
        align-items: center;
        border-radius: 50px;
        color: #fff;
        cursor: pointer;
        &:hover {
          background-color: blue;
        }
      }
      /deep/.el-input__inner {
        width: 150px;
      }
    }
    .elbtn {
      padding: 5px 30px;
      border-radius: 10px;
    }
    .table {
      .img {
        width: 40px;
        height: 40px;
      }
    }
  }
}
</style>