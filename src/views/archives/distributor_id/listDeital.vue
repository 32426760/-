<template>
  <div class="ListDeital">
    <div class="main">
      <div class="left">
        <div class="main_left">
          <div class="main_left_img">
            <img :src="obj.cardpicurl" alt />
          </div>
          <div class="main_left_deital">
            <div class="main_left_deital_name">{{obj.companyname}}</div>
            <div>
              <div>
                <div v-for="(item, index) in obj.contact_data" :key="index">
                  <span style="margin:0 10px">{{item.contacts}}:</span>
                  <span>{{item.phone}}</span>
                </div>
              </div>
            </div>
            <div>
              账号信息：
              <div>
                <div v-for="(item, index) in obj.bank_data" :key="index">
                  <span>{{item.bank}}</span>
                  <span style="margin:0 10px">{{item.bankid}}</span>
                  <span>{{item.name}}</span>
                </div>
              </div>
            </div>
            <div>{{obj.address}}</div>
          </div>
        </div>
        <div class="main_left">
          <div class="main_left_img">
            <img :src="obj.compicurl" alt />
          </div>
          <div class="main_left_deital">
            <div>是否开发票：{{obj.isbill}}</div>
            <div>税点：{{obj.tax}}</div>
            <div>面料统计：{{obj.material_count}}</div>
            <div>成交笔数：{{obj.deal_count}}</div>
            <div>修改人：{{obj.user_name}}</div>
            <div>修改时间：{{obj.ctime}}</div>
            <div>备注:{{obj.remarks}}</div>
          </div>
        </div>
      </div>
      <router-link :to="`/EditSupplier?id=${obj.id}`" :data="obj">
        <span class="el-icon-edit" style="font-size: 30px;cursor: pointer;"></span>
      </router-link>
    </div>
  </div>
</template>

<script>
import { getSupplierInfo } from "@/api/archives";
export default {
  data() {
    return {
      id: "",
      obj: {}
    };
  },
  async mounted() {
    let { id } = this.$route.query;
    console.log(id);
    let res = await getSupplierInfo({ id });
    this.obj = res.data.data;
    console.log(res);
    console.log(this.obj.isbill);
    if (this.obj.isbill === "0") {
      this.obj.isbill = "开";
    }
    if (this.obj.isbill === "1") {
      this.obj.isbill = "不开";
    }
  }
};
</script>

<style lang="less" scoped>
.ListDeital {
  
  .main {
    display: flex;
    justify-content: space-between;
    padding: 20px;
    font-size: 14px;
    .main_left {
      display: flex;
      margin-bottom: 50px;
      .main_left_img {
        margin-right: 20px;
        img {
          width: 200px;
          height: 200px;
        }
      }
      .main_left_deital {
        .main_left_deital_name {
          font-size: 16px;
          font-weight: 600;
        }
        div {
          margin: 5px 0px;
        }
      }
    }
    .main_right {
    }
  }
}
</style>