<template>
  <div class="materialProcess">
    <div class="main">
      <!-- 增加款式颜色 -->
      <div style="display:flex">
        <div class="color_num" v-for="(item, index) in obj.style_color_data" :key="index">
          <div
            style="display: flex;justify-content: center;align-items: center;"
            @click="handleColorNum(item,index)"
            :class="active===index?'active':''"
          >
            <div class="color">{{item.style_color_name}}</div>
            <div class="el-icon-close" @click.stop="styleColorDel(item)"></div>
          </div>
        </div>
        <div class="addColor" @click="addKindColor">增加款式颜色</div>
        <!--  -->
      </div>
      <!-- 数据 -->
      <div v-if="style_color_data_length!==0">
        <div class="cardList" v-for="(item, index) in cardList" :key="index">
          <div style="display: flex;justify-content: space-between;align-items: flex-end;">
            <div>
              <div v-for="(item1, index1) in card" :key="index1">
                <div v-for="(item2, index2) in item1.style_materials_data" :key="index2">
                  <div class="card" v-if="item.materials===item1.mainclass" style="margin:10px 0">
                    <div class="cardStyle">
                      <div class="cardStyle_left">
                        <div class="cardStyle_left_img">
                          <img :src="item2.picurl" alt />
                        </div>
                        <div class="cardStyle_left_content">
                          <div class="cardStyle_left_content_name">
                            <div>{{item2.mainclass}}</div>
                            <div
                              class="el-icon-close"
                              style="cursor: pointer;"
                              @click.stop="handleStyleMaterialsDel(item2)"
                            ></div>
                          </div>
                          <div>{{item2.color}}</div>
                          <div>内部编号:895565562223</div>
                          <div>某某布行</div>
                        </div>
                      </div>
                      <div class="cardStyle_right" @mouseleave="visible2 = false">
                        <div style="cursor: pointer;" @click="handlePopoverId2(item2)">
                          <el-popover
                            placement="right"
                            v-model="visible2"
                            v-if="item2.id===popoverId2"
                          >
                            <div class="colourNumberList">
                              <div
                                class="colourNumber"
                                @click.stop="handleColourNumber2(item2,item3)"
                                v-for="(item3, index3) in item2.materials_color_data"
                                :key="index3"
                              >
                                <img :src="item3.picurl" alt />
                                <div>{{item3.color}} {{item3.color_no}}</div>
                              </div>
                            </div>
                          </el-popover>
                          <div>{{item2.color||item2.materials_color_data[0].color}}</div>
                          <div>{{item2.color_no||item2.materials_color_data[0].color_no}}</div>
                        </div>
                        <el-checkbox v-model="item2.isCheckList1" @change="isCheckListBox1(item2)"></el-checkbox>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <el-button
              class="cardBtn"
              size="mini"
              round
              @click="handleMaterialsCard(item)"
            >添加{{item.materialsCard}}</el-button>
          </div>
          <el-divider content-position="right">{{item.materials}}</el-divider>
        </div>
      </div>
      <div class="del_purchase_note">
        <el-button size="mini" round @click="purchaseOrder">生成采购单</el-button>
      </div>
      <!-- 删除历史 -->
      <div class="del_history">
        <div class="operation">
          <div>删除历史</div>
        </div>
        <div v-for="(item, index) in delListData" :key="index">
          <div class="cardStyle" v-for="(item1, index1) in item.style_materials_data" :key="index1">
            <div class="cardStyle_left">
              <div class="cardStyle_left_img">
                <img :src="item.picurl" alt />
              </div>
              <div class="cardStyle_left_content">
                <div class="cardStyle_left_content_name">面料</div>
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
              <div class="restore" @click="handleRestore(item1)">还原</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <el-dialog title="增加款式颜色" :visible.sync="centerDialogVisible" width="30%" center class="dialog">
      <el-input v-model="designColor" placeholder="请输入内容" style="width:200px"></el-input>
      <div v-if="style_color_data_length!==0">
        <div class="cardList" v-for="(item, index) in cardList" :key="index">
          <div style="display: flex;justify-content: space-between;align-items: flex-end;">
            <div>
              <div v-for="(item1, index1) in searchCard" :key="index1">
                <div v-for="(item2, index2) in item1.style_materials_data" :key="index2">
                  <div class="card" v-if="item.materials===item1.mainclass" style="margin:10px 0">
                    <div class="cardStyle">
                      <div class="cardStyle_left">
                        <div class="cardStyle_left_img">
                          <img :src="item2.picurl" alt />
                        </div>
                        <div class="cardStyle_left_content">
                          <div class="cardStyle_left_content_name">
                            <div>{{item2.mainclass}}</div>
                          </div>
                          <div>{{item2.color}}</div>
                          <div>内部编号:895565562223</div>
                          <div>某某布行</div>
                        </div>
                      </div>
                      <div class="cardStyle_right" @mouseleave="visible1 = false">
                        <div style="cursor: pointer;" @click.stop="handlePopoverId1(item2)">
                          <el-popover
                            placement="right"
                            width="100"
                            v-model="visible1"
                            v-if="item2.id===popoverId1"
                          >
                            <div class="colourNumberList">
                              <div
                                class="colourNumber"
                                @click.stop="handleColourNumber1(item2,item3)"
                                v-for="(item3, index3) in item2.materials_color_data"
                                :key="index3"
                              >
                                <img :src="item3.picurl" alt />
                                <div>{{item3.color}} {{item3.color_no}}</div>
                              </div>
                            </div>
                          </el-popover>
                          <div>{{item2.color||item2.materials_color_data[0].color}}</div>
                          <div>{{item2.color_no||item2.materials_color_data[0].color_no}}</div>
                        </div>
                        <el-checkbox v-model="item2.isCheckList" @change="isCheckListBox(item2)"></el-checkbox>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <el-divider content-position="right">{{item.materials}}</el-divider>
        </div>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="centerDialogVisible = false">取 消</el-button>
        <el-button @click="addDesignColor">确 定</el-button>
      </span>
    </el-dialog>
    <!-- 增加物料 -->
    <el-dialog title="新增物料" :visible.sync="centerDialogVisible1" width="60%" center class="dialog1">
      <el-input
        v-model="searchInput"
        @input="handleSearchInput"
        placeholder="请输入内容"
        style="width:300px"
      ></el-input>
      <div class="searchCard">
        <div class="card" v-for="(item, index) in MaterialsList" :key="index">
          <div class="cardStyle">
            <div class="cardStyle_left" @click="addMaterialsList(item)">
              <div class="cardStyle_left_img">
                <img :src="item.picurl" alt />
              </div>
              <div class="cardStyle_left_content">
                <div class="cardStyle_left_content_name">
                  <div>{{item.materialsname}}</div>
                </div>
                <div>水印花系列</div>
                <div>内部编号:895565562223</div>
                <div>某某布行</div>
              </div>
            </div>
            <div class="cardStyle_right" @mouseleave="visible = false">
              <div style="cursor: pointer;" @click="handlePopoverId(item)">
                <el-popover width="100" v-model="visible" v-if="popoverId===item.id">
                  <div class="colourNumberList">
                    <div
                      class="colourNumber"
                      @click.stop="handleColourNumber(item,item1)"
                      v-for="(item1, index1) in item.materials_color_data"
                      :key="index1"
                    >
                      <img :src="item1.picurl" alt />
                      <div>{{item1.color}} {{item1.color_no}}</div>
                    </div>
                  </div>
                </el-popover>
                <div>{{item.color||item.materials_color_data[0].color}}</div>
                <div>{{item.color_no||item.materials_color_data[0].color_no}}</div>
              </div>
            </div>
          </div>
        </div>
      </div>
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
    </el-dialog>
  </div>
</template>

<script>
import {
  getStyle,
  projectStyleColorDel,
  projectStyleColorAdd,
  getStyleMaterialsList,
  getMaterialsList,
  projectStyleMaterialsAdd,
  getStyleMaterialsDellist,
  projectStyleMaterialsHfdel,
  materialsProcureAdd,
  projectStyleMaterialsDel
} from "@/api/researchDevelopment";
export default {
  data() {
    return {
      designColor: "",
      obj: {},
      centerDialogVisible: false, //增加款式颜色
      centerDialogVisible1: false, //增加款式颜色
      value: "",
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
      card: [], //首页数据
      searchCard: [], //搜索数据
      visible: false,
      visible1: false,
      visible2: false,
      colourNumberId: "",
      isCheckList: [], //复选框数组
      isCheckList1: [], //复选框数组1
      searchInput: "", //搜索值
      pageIndex: 1,
      pageSize: 10,
      total: 0,
      MaterialsList: [], //物料数组
      style_color_data_length: "", //样式颜色数据长度
      popoverId: "", //弹出框id
      popoverId1: "", //弹出框id1
      popoverId2: "", //弹出框id1
      style_id: "", //样式ID
      style_color_name: "", //样式颜色id
      materials: "", //物料
      materials_color_id: "", //物料颜色id
      materials_color_id1: "", //物料颜色id
      materials_color_id2: "", //物料颜色id
      isCheckListBoxEvent: {},
      delListData: [],
      active: 0
    };
  },
  methods: {
    async handleRestore(item1) {
      let res = await projectStyleMaterialsHfdel({ id: item1.id });
      console.log(res);
      this.init();
      this.delListInit();
    },
    async addKindColor() {
      this.centerDialogVisible = true;
      // 列表数据
      if (this.obj.style_color_data.length > 0) {
        this.style_id = this.obj.style_color_data[0].style_id;
        this.style_color_name = this.obj.style_color_data[0].style_color_name;
        let res1 = await getStyleMaterialsList({
          style_id: this.style_id,
          style_color_name: this.style_color_name
        });
        res1.data.data.forEach((v, i) => {
          v.style_materials_data.forEach((v, i) => {
            v["isCheckList"] = false;
          });
        });
        let { data } = res1.data;
        this.searchCard = data;
        this.style_color_data_length = this.obj.style_color_data.length;
        this.designColor = "";
        this.isCheckList = [];
      }
    },
    async handleStyleMaterialsDel(item) {
      this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(async () => {
          let res = await projectStyleMaterialsDel({ id: item.id });
          this.active = 0;
          this.init();
          this.delListInit();
          this.$message({
            type: "success",
            message: "删除成功!"
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    },
    async addMaterialsList(item) {
      console.log(this.style_id);
      console.log(this.style_color_name);
      console.log(this.materials);
      let style_id = this.style_id;
      let style_color_name = this.style_color_name;
      let mainclass = this.materials;
      let materials_id = item.id;
      let materials_color_id =
        this.materials_color_id || item.materials_color_data[0].id;
      let res = await projectStyleMaterialsAdd({
        style_id,
        style_color_name,
        mainclass,
        materials_id,
        materials_color_id
      });
      console.log(res);
      this.active = 0;
      this.init();
      this.centerDialogVisible1 = false;
    },
    handleColourNumber(item, item1) {
      this.materials_color_id = item1.id;
      item["color"] = item1.color;
      item["color_no"] = item1.color_no;
      this.visible = false;
    },
    handleColourNumber1(item2, item3) {
      console.log(item3);
      this.materials_color_id1 = item3.id;
      item2["color"] = item3.color;
      item2["color_no"] = item3.color_no;
      this.visible1 = false;
    },
    async handleColourNumber2(item2, item3) {
      this.materials_color_id2 = item3.id;
      item2["color"] = item3.color;
      item2["color_no"] = item3.color_no;
      let res = await styleMaterialsListColorEdit({
        id: item2.id,
        materials_color_id: item3.id
      });
      this.visible2 = false;
    },
    handlePopoverId(item) {
      this.popoverId = item.id;
      this.visible = true;
    },
    handlePopoverId1(item) {
      console.log(item);
      this.popoverId1 = item.id;
      this.visible1 = true;
    },
    handlePopoverId2(item) {
      this.popoverId2 = item.id;
      this.visible2 = true;
    },
    async handleSearchInput() {
      let res = await getMaterialsList({
        keyword: this.searchInput,
        page: this.pageIndex,
        page_size: this.pageSize
      });
      let { data } = res.data;
      this.MaterialsList = data;
    },
    handleMaterialsCard(item) {
      this.searchInput = "";
      this.materials = item.materials;
      this.centerDialogVisible1 = true;
    },
    async styleColorDel(item) {
      this.$confirm("此操作将永久删除该文件, 是否继续?", "提示", {
        confirmButtonText: "确定",
        cancelButtonText: "取消",
        type: "warning"
      })
        .then(async () => {
          let { id } = this.$route.query;
          let res = await projectStyleColorDel({
            style_id: id,
            style_color_name: item.style_color_name
          });
          this.init();
          this.$message({
            type: "success",
            message: "删除成功!"
          });
        })
        .catch(() => {
          this.$message({
            type: "info",
            message: "已取消删除"
          });
        });
    },
    async addDesignColor() {
      if (this.isCheckListBoxEvent.isCheckList !== true) {
        let { id } = this.$route.query;
        let res = await projectStyleColorAdd({
          style_id: id,
          style_color_name: this.designColor
        });
        this.init();
        this.centerDialogVisible = false;
        this.designColor = "";
      }
      if (this.isCheckListBoxEvent.isCheckList === true) {
        let obj = {};
        obj["style_color_name"] = this.designColor;
        obj["style_materials_data"] = this.isCheckList;
        let res = await projectStyleColorAdd(obj);
        console.log(res);
        this.init();
        this.active = 0;
        this.centerDialogVisible = false;
      }
    },
    isCheckListBox(e) {
      this.isCheckListBoxEvent = e;
      if (e.isCheckList === true) {
        this.isCheckList.push({
          mainclass: e.mainclass,
          style_materials_data: {
            materials_color_id:
              this.materials_color_id1 || e.materials_color_data[0].id,
            style_id: e.style_id,
            materials_id: e.materials_id
          }
        });
      }
      if (e.isCheckList === false) {
        this.isCheckList.pop();
      }
    },
    isCheckListBox1(e) {
      // console.log(e);
      if (e.isCheckList1 === true) {
        this.isCheckList1.push({
          style_materials_list_id: e.id,
          materials_color_id: this.materials_color_id2 || e.style_color_id
        });
      }
      if (e.isCheckList1 === false) {
        this.isCheckList1.pop();
      }
    },
    async handleColorNum(item, index) {
      this.active = index;
      console.log(item);
      this.style_id = item.style_id;
      this.style_color_name = item.style_color_name;
      let res = await getStyleMaterialsList({
        style_id: item.style_id,
        style_color_name: item.style_color_name
      });
      if (res.data.data.length !== 0) {
        res.data.data.forEach((v, i) => {
          v.style_materials_data.forEach((v, i) => {
            v["isCheckList"] = false;
          });
        });
      }
      let { data } = res.data;
      console.log(data);
      this.card = data;
    },
    colourNumber(item2) {
      this.colourNumberId = item2.id;
      this.visible = true;
    },
    async purchaseOrder() {
      let { id } = this.$route.query;
      let obj = {};
      obj["materials_data"] = this.isCheckList1;
      let res = await materialsProcureAdd(obj);
      console.log(res);
      this.$router.push({ path: `/materialPurchasing?id=${id}` });
    },
    async init() {
      let { id } = this.$route.query;
      let res = await getStyle({ id });
      this.obj = res.data.data;
      if (this.obj.style_color_data.length > 0) {
        // 列表数据
        this.style_id = this.obj.style_color_data[0].style_id;
        this.style_color_name = this.obj.style_color_data[0].style_color_name;
        let res1 = await getStyleMaterialsList({
          style_id: this.style_id,
          style_color_name: this.style_color_name
        });
        res1.data.data.forEach((v, i) => {
          v.style_materials_data.forEach((v, i) => {
            v["isCheckList"] = false;
          });
        });
        console.log(res1);
        let { data } = res1.data;
        this.card = data;
      }
      this.style_color_data_length = this.obj.style_color_data.length;
    },
    async delListInit() {
      let { id } = this.$route.query;
      let res = await getStyleMaterialsDellist({ style_id: id });
      console.log(res);
      let { data } = res.data;
      this.delListData = data;
    },
    handleSizeChange(val) {
      this.pageSize = val;
    },
    handleCurrentChange(val) {
      this.pageIndex = val;
    }
  },
  mounted() {
    this.init();
    this.delListInit();
  }
};
</script>

<style lang="less" scoped>
.materialProcess {
  .main {
    .color_num {
      margin: 0 30px;
      font-size: 14px;
      cursor: pointer;
      .color {
        margin-right: 10px;
      }
    }
    .addColor {
      cursor: pointer;
    }
    .cardList {
      margin: 30px 0;
      .card {
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
            .colourNumberList {
              .colourNumber {
                display: flex;
                justify-content: space-around;
                align-items: center;
                padding: 10px;
                cursor: pointer;
                border-bottom: 1px solid #ccc;
              }
              img {
                width: 30px;
                height: 30px;
              }
            }
          }
        }
      }
    }
    .del_purchase_note {
      padding: 30px 0;
      text-align: right;
      border-bottom: 1px solid #dcdfe6;
    }
    .del_history {
      .operation {
        padding: 20px 5px;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }
      .cardStyle {
        width: 320px;
        height: 100px;
        display: flex;
        margin: 10px 0;
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
              margin: 5px;
            }
            .cardStyle_left_content_name {
              font-weight: 600;
              font-size: 14px;
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
          .restore {
            cursor: pointer;
          }
        }
      }
    }
  }
  .dialog {
    .cardList {
      margin: 30px 0;
      .card {
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
            .colourNumberList {
              .colourNumber {
                display: flex;
                justify-content: space-around;
                align-items: center;
                padding: 10px;
                cursor: pointer;
              }
              img {
                width: 30px;
                height: 30px;
              }
            }
          }
        }
      }
    }
  }
  .dialog1 {
    .searchCard {
      display: flex;
      flex-wrap: wrap;
      align-items: center;
      .card {
        margin: 10px 20px;
        display: flex;
        justify-content: space-around;
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
              }
            }
          }
          .cardStyle_right {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 50px;
            background-color: #f2f2f2;
            border-radius: 10px;
            .colourNumberList {
              .colourNumber {
                display: flex;
                justify-content: space-around;
                align-items: center;
                padding: 10px;
                cursor: pointer;
              }
              img {
                width: 30px;
                height: 30px;
              }
            }
          }
        }
      }
    }
  }
  .active {
    border: 1px solid #000;
  }
}
</style>