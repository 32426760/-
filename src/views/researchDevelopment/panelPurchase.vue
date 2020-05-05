<template>
  <div class="panelPurchase">
    <!-- 面包屑 -->
    <el-breadcrumb separator="/" class="breadcrumb">
      <img src="../../assets/mbxlogo.svg" alt class="mbxlogo" />
      <el-breadcrumb-item>研发部</el-breadcrumb-item>
      <el-breadcrumb-item>版料采购</el-breadcrumb-item>
      <el-breadcrumb-item>版料采购单</el-breadcrumb-item>
    </el-breadcrumb>
    <div class="main">
      <!-- 物料卡信息 供应商信息 -->
      <div class="info">
        <div style="display: flex;">
          <div class="cardInfo">
            <div class="cardInfoTitle">物料卡信息</div>
            <div class="cardInfoContent">
              <div class="cardInfoContentImg">
                <img
                  src="https://axure-file.lanhuapp.com/b0e7ed9c-a55b-4903-972b-002bbf42cf81__18e91cdafc56e4c42b9b7f738728a2cd.svg"
                  alt
                />
              </div>
              <div class="cardInfoContentText">
                <div class="cardInfoContentTextName">水印花衬衣</div>
                <div style="display: flex;">
                  <div style="margin-right:100px">
                    <div>内部编号</div>
                    <div>编号</div>
                    <div>面料分类</div>
                    <div>料属性</div>
                    <div style="display: flex;">
                      <div style="margin-right:10px">面料成分</div>
                      <div>
                        <div>生纱 33%</div>
                        <div>生纱 33%</div>
                        <div>生纱 33%</div>
                      </div>
                    </div>
                  </div>
                  <div>
                    <div>色号：</div>
                    <div>颜色：杏色</div>
                    <div>大货单价：</div>
                    <div>幅宽：</div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="supplierInfo">
            <div class="supplierInfoTitle">物料卡信息</div>
            <div class="supplierInfoContent">
              <div class="supplierInfoContentImg">
                <img
                  src="https://axure-file.lanhuapp.com/b0e7ed9c-a55b-4903-972b-002bbf42cf81__44165dbf31a07f62bf2168628c160f13.svg"
                  alt
                />
              </div>
              <div class="supplierInfoContentText">
                <div class="supplierInfoContentTextName">某某布行</div>
                <div>13570383596</div>
                <div>020-89261869</div>
                <div>账号信息：</div>
                <div>广东省广州市海珠区中大九洲广场纬一街北区1020档</div>
                <div></div>
              </div>
            </div>
          </div>
        </div>
        <div class="purchaseInfo">
          <div class="purchaseInfoTitle">采购信息</div>
          <div class="userProfile">
            <span style="padding:10px 30px">
              事件号：
              自动生成
            </span>
            <span>
              经办人：
              自动生成
            </span>
          </div>
          <div class="form">
            <el-form ref="form" :model="form" label-width="100px">
              <el-form-item label="用量">
                <el-col :span="6">
                  <el-input v-model="form.name" style="width:200px"></el-input>
                </el-col>
                <el-col :span="6">
                  <el-button size="small" round @click="readyforTheCall">备货调用</el-button>
                </el-col>
              </el-form-item>
              <el-form-item label="采购量">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="采购单价">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="金额">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="订金">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="支付方式">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="预计回料时间">
                <el-input v-model="form.name" style="width:200px"></el-input>
              </el-form-item>
              <el-form-item label="上传凭证">
                <el-upload
                  class="avatar-uploader"
                  action="https://yj.ppp-pay.top/uploadpic.php"
                  :show-file-list="false"
                  :on-success="handleAvatarSuccess"
                  :before-upload="beforeAvatarUpload"
                >
                  <img v-if="picurl" :src="picurl" class="avatar" />
                  <i v-else class="el-icon-upload avatar-uploader-icon"></i>
                </el-upload>
              </el-form-item>
              <el-form-item>
                <el-button round @click="onSubmit">保存</el-button>
              </el-form-item>
            </el-form>
          </div>
        </div>
      </div>
    </div>
    <el-dialog title="增加款式颜色" :visible.sync="centerDialogVisible" width="30%" center class="dialog">
      aa
      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="centerDialogVisible = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: ""
      },
      picurl: "",
      centerDialogVisible: false
    };
  },
  methods: {
    readyforTheCall() {
      this.centerDialogVisible = true;
    },
    onSubmit() {
      console.log("submit!");
    },
    handleAvatarSuccess(res, file) {
      this.picurl = res.data.pic_file_url;
      console.log(this.picurl);
    },
    beforeAvatarUpload(file) {
      // console.log(file)
      const isJPG = file.type === "image/jpeg";
      const isLt2M = file.size / 1024 / 1024 < 2;

      if (!isJPG) {
        this.$message.error("上传头像图片只能是 JPG 格式!");
      }
      if (!isLt2M) {
        this.$message.error("上传头像图片大小不能超过 2MB!");
      }
      return isJPG && isLt2M;
    }
  }
};
</script>

<style lang="less" scoped>
.panelPurchase {
  .main {
    .info {
      .cardInfo {
        margin-right: 80px;
        .cardInfoTitle {
          padding: 30px 10px;
          font-size: 16px;
        }
        .cardInfoContent {
          display: flex;
          .cardInfoContentImg {
            margin-right: 30px;
            img {
              width: 200px;
              height: 200px;
            }
          }
          .cardInfoContentText {
            div {
              margin: 3px 0;
              font-size: 14px;
            }
            .cardInfoContentTextName {
              font-size: 16px;
              font-weight: 600;
              margin-top: 10px;
            }
          }
        }
      }
      .supplierInfo {
        .supplierInfoTitle {
          padding: 30px 10px;
          font-size: 16px;
        }
        .supplierInfoContent {
          display: flex;
          .supplierInfoContentImg {
            img {
              width: 200px;
              height: 200px;
            }
          }
          .supplierInfoContentText {
            margin: 10px 30px;
            div {
              margin: 3px 0;
              font-size: 14px;
            }
            .supplierInfoContentTextName {
              font-size: 16px;
              font-weight: 600;
              margin-top: 10px;
            }
          }
        }
      }
      .purchaseInfo {
        .purchaseInfoTitle {
          padding: 30px 10px;
          font-size: 16px;
        }
      }
      .form {
        margin: 30px 10px;
      }
    }
  }
  
}
</style>