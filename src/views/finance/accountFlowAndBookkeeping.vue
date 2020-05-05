<template>
  <div class="accountFlowAndBookkeeping">
     <el-breadcrumb separator="/" class="breadcrumb">
      <img src="../../assets/mbxlogo.svg" alt class="mbxlogo" />
      <el-breadcrumb-item>财务</el-breadcrumb-item>
      <el-breadcrumb-item>账户流水及记账</el-breadcrumb-item>
    </el-breadcrumb>

    <div class="condition clearfix">
      <div class="date fl">
        <label for>日期：</label>
        <el-date-picker
          v-model="date"
          type="daterange"
          range-separator="至"
          :start-placeholder="ctime_start"
          :end-placeholder="ctime_end"
        ></el-date-picker>
      </div>
      <div class="accountType fl">
        <label for>账目类型：</label>
        <el-select v-model="category" placeholder="类别">
          <el-option
            v-for="item in categorys"
            :key="item.id"
            :label="item.style_type"
            :value="item.style_type"
          ></el-option>
        </el-select>
      </div>
      <div class="settlement fl">
        <label for>结算账户：</label>
        <el-select v-model="category" placeholder="类别">
          <el-option
            v-for="item in categorys"
            :key="item.id"
            :label="item.style_type"
            :value="item.style_type"
          ></el-option>
        </el-select>
      </div>
      <div class="odd fl">
        <label for>单号：</label>
        <el-input
          placeholder="单据编号"
          v-model="input"
          clearable>
        </el-input>
      </div>
      <div class="stylist fl">
        <label for>操作者：</label>
        <el-select v-model="stylist" placeholder="- 全部 -" @change="handleUser_id($event)">
          <el-option v-for="item in stylists" :key="item.id" :label="item.name" :value="item.id"></el-option>
        </el-select>
      </div>
      <div class="category fl">
        <label for>类别：</label>
        <el-select v-model="category" placeholder="类别">
          <el-option
            v-for="item in categorys"
            :key="item.id"
            :label="item.style_type"
            :value="item.style_type"
          ></el-option>
        </el-select>
      </div>
       
      <div class="btn fl" @click="handlesearch">
        <el-button icon="el-icon-search">搜索</el-button>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";
import {
  getDataList,
  getYearList,
  getSeasonList,
  getStylistList,
  getCategoryList,
} from "@/api/researchDevelopment";
export default {
  
  data(){
    return{
      data: [],
      years: [],
      seasons: [],
      stylists: [],
      categorys: [],
      wests: [],
      date: "", //日期
      name: "", //名称
      year: "", //年
      season: "", //季节
      stylist: "", //设计师
      category: "", //类别
      west: "", //西所
      state: "", //状态
      ctime_start: "",
      ctime_end: "",
      pageIndex: 1,
      pageSize: 9,
      total: 0,
      user_id: "",
      customer_id: "",
      stateId: "",
      input:'',
    }
  },
  methods:{
    handleUser_id(e) {
      this.user_id = e;
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
     // 搜索
    async handlesearch() {
      var obj = {};
      // console.log(...this.date)
      obj["ctime_start"] = moment(this.date[0]).format("YYYY-MM-DD");
      obj["ctime_end"] = moment(this.date[1]).format("YYYY-MM-DD");
      obj["stylekeyword"] = this.name;
      obj["year"] = this.year;
      obj["season"] = this.season;
      obj["user_id"] = this.user_id;
      obj["style_type"] = this.category;
      obj["customer_id"] = this.customer_id;
      obj["state"] = this.stateId;
      delete obj["0"];
      delete obj["1"];
      this.init(obj);
    },
    async init(obj) {
      let res = await getDataList({
        page: this.pageIndex,
        page_size: this.pageSize,
        ...obj
      });
      console.log(res);
      let { data, count } = res.data;
      this.data = data;
      this.total = count;
      this.ctime_start = moment(this.date[0]).format("YYYY-MM-DD");
      this.ctime_end = moment(this.date[1]).format("YYYY-MM-DD");
    }
  },
  mounted(){
    this.init();
    this.getYear();
    this.getSeason();
    this.getStylist();
    this.getCategory();
  }
  
}
</script>

<style lang="less" scoped>
  .accountFlowAndBookkeeping{
    label {
      width: 40px;
      margin-right: 10px;
    }
    .condition {
      padding: 20px 100px 30px 20px;
      /deep/.el-input__inner {
        width: 380px;
      }
      .stylist {
        margin-top: 10px;
        /deep/.el-input__inner {
          width: 140px !important;
        }
      }
      .category {
        margin-top: 10px;
        /deep/.el-input__inner {
          width: 100px !important;
        }
      }
      .odd {
        display: flex;
        margin-top: 10px;
        label{
          width: 55px;
          display: flex;
          justify-content: center;
          align-items: center;
        }
        /deep/.el-input__inner {
          width: 200px !important;
        }
      }
      .accountType {
        margin-top: 10px;
        /deep/.el-input__inner {
          width: 100px !important;
        }
      }
      .settlement {
        margin-top: 10px;
        /deep/.el-input__inner {
          width: 100px !important;
        }
      }
      
      .btn,.date {
        margin-top: 10px;
      }
    }
  }
</style>