<template>
  <div class="materialPurchasing">
    <div class="material_purchase_name">
      <div
        v-for="(item, index) in obj.style_color_data"
        :key="index"
        style="display: flex;align-items: center;"
      >
        <el-divider direction="vertical"></el-divider>
        <div
          style="margin:0 10px;cursor: pointer;"
          @click="handleColorNum(item,index)"
          :class="active===index?'active':''"
        >{{item.style_color_name}}</div>
        <el-divider direction="vertical"></el-divider>
      </div>
    </div>
    <div v-for="(item, index) in style_materials" :key="index">
      <div class="content" v-for="(item1, index1) in item.style_materials_data" :key="index1">
        <div class="card">
          <div class="cardStyle">
            <div class="cardStyle_left">
              <div class="cardStyle_left_img">
                <img :src="item1.picurl" alt />
              </div>
              <div class="cardStyle_left_content">
                <div class="cardStyle_left_content_name">
                  <div>面料</div>
                  <div class="el-icon-close"></div>
                </div>
                <div>水印花系列</div>
                <div>内部编号:895565562223</div>
                <div>某某布行</div>
              </div>
            </div>
            <div class="cardStyle_right">
              <div>
                {{item1.color}}
                <div>{{item1.color_no}}</div>
              </div>
            </div>
          </div>
        </div>
        <div class="orderInformation">
          <el-steps space="500" style="margin-top:50px">
            <el-step
              style="width:100px"
              :title="item.logname"
              :description="item.ctime"
              v-for="(item, index) in activities_endlong"
              :key="index"
            ></el-step>
          </el-steps>
          <div>
            <el-button size="mini" round @click="goPanelPurchase">{{item.materialsCard}}</el-button>
          </div>
        </div>
      </div>
      <el-divider content-position="right">{{item.mainclass}}</el-divider>
    </div>
  </div>
</template>

<script>
import { getStyle, getMaterialsProcureList } from "@/api/researchDevelopment";
export default {
  data() {
    return {
      cardList: [
        {
          materialsCard: "主料卡",
          materials: "主料"
        },
        {
          materialsCard: "里料卡",
          materials: "里料"
        },
        {
          materialsCard: "辅料卡",
          materials: "辅料"
        },
        {
          materialsCard: "工艺卡",
          materials: "工艺"
        }
      ], //首页大数据
      activities_endlong: [], //日志
      obj: {},
      style_materials: [],
      active: 0
    };
  },
  methods: {
    handleColorNum(item, index) {
      this.active = index;
    },
    goPanelPurchase() {
      this.$router.push({ name: "PanelPurchase" });
    },
    async init() {
      let { id } = this.$route.query;
      let res = await getStyle({ id });
      this.obj = res.data.data;
      console.log(this.obj);
      let res1 = await getMaterialsProcureList({
        style_id: this.obj.style_color_data[0].style_id,
        style_color_name: this.obj.style_color_data[0].style_color_name
      });
      let { data } = res1.data;
      this.style_materials = data;
      console.log(res1);
    }
  },
  mounted() {
    this.init();
  }
};
</script>

<style lang="less" scoped>
.materialPurchasing {
  .material_purchase_name {
    font-size: 16px;
    margin-bottom: 10px;
    display: flex;
  }
  .content {
    display: flex;
    margin: 10px 0px;
    .card {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      .cardStyle {
        width: 320px;
        height: 100px;
        display: flex;
        .cardStyle_left {
          width: 270px;
          display: flex;
          background-color: #f2f2f2;
          border-radius: 10px;
          .cardStyle_left_img {
            img {
              width: 100px;
              height: 100px;
            }
          }
          .cardStyle_left_content {
            flex: 1;
            div {
              margin: 3px;
            }
            .cardStyle_left_content_name {
              font-weight: 600;
              font-size: 14px;
              display: flex;
              justify-content: space-between;
              .el-icon-close {
                cursor: pointer;
              }
            }
          }
        }
        .cardStyle_right {
          display: flex;
          flex-direction: column;
          justify-content: space-around;
          align-items: center;
          width: 50px;
          background-color: #f2f2f2;
          border-radius: 10px;
        }
      }
    }
    .orderInformation {
      border-radius: 10px;
      background-color: #f2f2f2;
      width: 600px;
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      height: 100px;
      padding: 10px;
    }
  }
  .active {
    border-bottom: 1px solid aqua;
    color: aqua;
  }
}
// patternStatus
// PatternStatus
</style>