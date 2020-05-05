<template>
  <div class="designFile">
    <!-- 面包屑 -->
    <el-breadcrumb separator="/" class="breadcrumb">
      <img src="../assets/mbxlogo.svg" alt class="mbxlogo" />
      <el-breadcrumb-item>档案库</el-breadcrumb-item>
      <el-breadcrumb-item>款式档案</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="main">
      <div class="info">
        <div class="basicsInfo">
          <div class="basicsInfoName">款式基础信息</div>
          <div class="basicsInfoImg">
            <img
              src="https://axure-file.lanhuapp.com/b0e7ed9c-a55b-4903-972b-002bbf42cf81__c2aebbdbcc56676ac75dab716738120a.svg"
              alt
            />
            <img
              src="https://axure-file.lanhuapp.com/b0e7ed9c-a55b-4903-972b-002bbf42cf81__c2aebbdbcc56676ac75dab716738120a.svg"
              alt
            />
          </div>
        </div>
        <div class="materialCardInfo">
          <div class="materialCardInfoName">物料卡信息</div>
          <div class="materialCardInfoContent">
            <div style="font-size:20px;font-weight: 600;">水印花衬衣</div>
            <div style="display:flex">
              <div style="margin-right:100px">
                <div>款号：2020898965</div>
                <div>品类：衬衣</div>
                <div>年份：2020</div>
                <div>季节：春</div>
                <div>颜色：杏色</div>
                <div>设计师：zaan</div>
              </div>
              <div>
                <div>物料总费：</div>
                <div>加工费：</div>
                <div>工艺费：</div>
                <div>总成本：</div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- 下单批次： -->
      <div class="placeAnOrderBatchInfo">
        <div class="placeAnOrderBatch">下单批次：1</div>
        <div class="placeAnOrderBatch">下单批次：2</div>
        <div class="placeAnOrderBatch">+ 增加批次</div>
      </div>
      <el-collapse v-model="activeNames" @change="handleChange">
        <el-collapse-item title="下单信息" name="1">
          <div class="orderInformation">
            <el-form ref="form" :model="form" label-width="80px">
              <el-form-item label="客户">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="颜色">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="总量">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="尺码">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="数量">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="比例">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="颜色">
                <el-select v-model="form.region" placeholder="请选择活动区域">
                  <el-option label="区域一" value="shanghai"></el-option>
                  <el-option label="区域二" value="beijing"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item>
                <el-button>确认下单</el-button>
              </el-form-item>
            </el-form>
          </div>
        </el-collapse-item>
        <el-collapse-item title="采购" name="2">
          <div class="purchase">
            <div class="color">
              <div>杏色</div>
              <div>黑色</div>
            </div>
            <div class="material_purchase">
              <div v-for="(item, index) in cardList" :key="index">
                <div class="content">
                  <div class="card">
                    <div class="cardStyle">
                      <div class="cardStyle_left">
                        <div class="cardStyle_left_img">
                          <img
                            src="https://axure-file.lanhuapp.com/b0e7ed9c-a55b-4903-972b-002bbf42cf81__07d4f05b25ce4b0e9a0dbdfec7c6ba15.svg"
                            alt
                          />
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
                          色号
                          <div>001</div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div class="wastage">
                    <div>
                      大货单件用量
                      <div>20m</div>
                    </div>
                    <div>
                      损耗
                      <div>0.5m</div>
                    </div>
                  </div>
                  <div class="amount">
                    <div>
                      计算总用量
                      <div>100m</div>
                    </div>
                    <div>
                      计算总金额
                      <div>10000</div>
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
                      <el-button size="mini" round>{{item.materialsCard}}</el-button>
                    </div>
                  </div>
                </div>
                <el-divider content-position="right">{{item.materials}}</el-divider>
              </div>
            </div>
            <el-button size="mini" round>超小按钮</el-button>
          </div>
        </el-collapse-item>
        <el-collapse-item title="生产排单" name="3">
          <div class="productionArranged">
            <el-form :inline="true" :model="formInline" class="demo-form-inline">
              <el-form-item label="指派工厂">
                <el-input v-model="formInline.user" placeholder="审批人" style="width:150px"></el-input>
              </el-form-item>
              <el-form-item label="指派方式">
                <el-select v-model="formInline.region" placeholder="活动区域" style="width:150px">
                  <el-option label="区域一" value="shanghai"></el-option>
                  <el-option label="区域二" value="beijing"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="指派数量">
                <el-select v-model="formInline.region" placeholder="活动区域" style="width:150px">
                  <el-option label="区域一" value="shanghai"></el-option>
                  <el-option label="区域二" value="beijing"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="加工价格">
                <el-select v-model="formInline.region" placeholder="活动区域" style="width:150px">
                  <el-option label="区域一" value="shanghai"></el-option>
                  <el-option label="区域二" value="beijing"></el-option>
                </el-select>
              </el-form-item>
              <el-form-item>
                <el-button>加工费对比</el-button>
              </el-form-item>
              <el-form-item>
                <el-input type="textarea" v-model="formInline.desc" style="width:60vw"></el-input>
              </el-form-item>
              <el-form-item>
                <el-button>确认排单</el-button>
              </el-form-item>
            </el-form>
          </div>
        </el-collapse-item>
        <el-collapse-item title="裁剪" name="4">
          <div class="tailor">
            <div>
              <el-row>
                <el-col :span="3">录入裁床数量：</el-col>
              </el-row>
              <el-row class="tailorList">
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>颜色</div>
                    <div style="margin:15px 0">杏色</div>
                    <div>杏色</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>S</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>M</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>L</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>数量</div>
                    <div style="margin:15px 0">100</div>
                    <div>100</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>总数</div>
                    <div style="margin:15px 0">200</div>
                    <div>200</div>
                  </div>
                </el-col>
              </el-row>
              <el-row class="tailorList">
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>颜色</div>
                    <div style="margin:15px 0">杏色</div>
                    <div>杏色</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>S</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>M</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>L</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>数量</div>
                    <div style="margin:15px 0">100</div>
                    <div>100</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>总数</div>
                    <div style="margin:15px 0">200</div>
                    <div>200</div>
                  </div>
                </el-col>
              </el-row>
            </div>
            <div class="add">
              <div>+增加床次</div>
              <el-button size="mini" round>超小按钮</el-button>
            </div>
          </div>
        </el-collapse-item>
        <el-collapse-item title="出货" name="5">
          <div class="shipment">
            <div class="shipmentList">
              <el-row>
                <el-col :span="3">出货数量：</el-col>
              </el-row>
              <el-row style="margin:20px 0">
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>成品</div>
                    <div style="margin:15px 0">杏色</div>
                    <div>杏色</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>S</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>M</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>L</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>数量</div>
                    <div style="margin:15px 0">100</div>
                    <div>100</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>总数</div>
                    <div style="margin:15px 0">200</div>
                    <div>200</div>
                  </div>
                </el-col>
              </el-row>
              <el-row>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>次品</div>
                    <div style="margin:15px 0">杏色</div>
                    <div>杏色</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>S</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>M</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>L</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>数量</div>
                    <div style="margin:15px 0">100</div>
                    <div>100</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>总数</div>
                    <div style="margin:15px 0">200</div>
                    <div>200</div>
                  </div>
                </el-col>
              </el-row>
            </div>
            <div class="shipmentList">
              <el-row>
                <el-col :span="3">出货数量：</el-col>
              </el-row>
              <el-row style="margin:20px 0">
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>成品</div>
                    <div style="margin:15px 0">杏色</div>
                    <div>杏色</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>S</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>M</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>L</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>数量</div>
                    <div style="margin:15px 0">100</div>
                    <div>100</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>总数</div>
                    <div style="margin:15px 0">200</div>
                    <div>200</div>
                  </div>
                </el-col>
              </el-row>
              <el-row>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>次品</div>
                    <div style="margin:15px 0">杏色</div>
                    <div>杏色</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>S</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>M</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>L</div>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                    <el-input v-model="input" placeholder="请输入内容"></el-input>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>数量</div>
                    <div style="margin:15px 0">100</div>
                    <div>100</div>
                  </div>
                </el-col>
                <el-col :span="3">
                  <div class="dfjccaic">
                    <div>总数</div>
                    <div style="margin:15px 0">200</div>
                    <div>200</div>
                  </div>
                </el-col>
              </el-row>
            </div>
            <div class="add">
              <div>+增加出货批次</div>
              <el-button size="mini" round>超小按钮</el-button>
            </div>
          </div>
        </el-collapse-item>
      </el-collapse>
    </div>
  </div>
</template>

<script>
import { getStyle } from "@/api/researchDevelopment";
export default {
  data() {
    return {
      input: "",
      activeNames: ["5"],
      form: {
        name: "",
        region: ""
      },
      formInline: {
        user: "",
        region: "",
        desc: ""
      },
      activities_endlong: [], //日志
      cardList: [
        {
          materialsCard: "面料卡",
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
      ],
      tailorList: []
    };
  },
  methods: {
    handleChange(val) {
      console.log(val);
    },
    onSubmit() {
      console.log("submit!");
    }
  },
  async mounted() {
    let { id } = this.$route.query;
    let res = await getStyle({ id });
    this.obj = res.data.data;
    console.log(this.obj);
    // console.log(this.obj.style_materials_color_data)
    this.activities_endlong = res.data.data.style_log;
  }
};
</script>
<style lang="less" scoped>
.designFile {
  .main {
    .info {
      display: flex;
      .basicsInfo {
        width: 40%;
        .basicsInfoName {
          margin: 30px 0px;
          font-size: 16px;
        }
        .basicsInfoImg {
          display: flex;
          img {
            width: 200px;
            margin-right: 20px;
          }
        }
      }
      .materialCardInfo {
        width: 40%;
        .materialCardInfoName {
          margin: 30px 0px;
          font-size: 16px;
        }
        .materialCardInfoContent {
          div {
            margin: 5px;
            font-size: 14px;
          }
        }
      }
    }
    .placeAnOrderBatchInfo {
      margin: 30px 0;
      display: flex;
      .placeAnOrderBatch {
        margin: 0 40px;
        font-size: 16px;
      }
    }
    .orderInformation {
    }
    .purchase {
      .color {
        display: flex;
        margin: 20px 0;
        div {
          margin: 0 40px;
        }
      }
      .material_purchase {
        .content {
          display: flex;
          .card {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            font-size: 12px;
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
                  div {
                    margin: 0 5px;
                  }
                  flex: 1;
                  .cardStyle_left_content_name {
                    font-weight: 600;
                    font-size: 14px;
                    display: flex;
                    justify-content: space-between;
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
          .wastage {
            width: 100px;
            border-radius: 10px;
            background-color: #f2f2f2;
            height: 100px;
            text-align: center;
          }
          .amount {
            width: 100px;
            border-radius: 10px;
            background-color: #f2f2f2;
            height: 100px;
            text-align: center;
          }
          .orderInformation {
            border-radius: 10px;
            background-color: #f2f2f2;
            width: 500px;
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            height: 100px;
            padding: 10px;
          }
        }
      }
    }
    .productionArranged {
      /deep/textarea {
        height: 100px;
        resize: none !important;
      }
    }
    .tailor {
      .tailorList {
        margin: 30px 0;
        padding: 10px 0;
        border-bottom: 1px solid #ccc;
      }
      .add {
        display: flex;
        justify-content: space-around;
        align-items: center;
      }
    }
    .shipment {
      .shipmentList {
        margin: 30px 0;
        padding: 10px 0;
        border-bottom: 1px solid #ccc;
      }
      .add {
        display: flex;
        justify-content: space-around;
        align-items: center;
      }
    }
  }
  .dfjccaic {
    display: flex;
    align-items: center;
    flex-direction: column;
    div {
      padding: 2px;
    }
  }
}
</style>


