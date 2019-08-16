<template>
  <div id="systemQuality_record">
    <div class="content">
      <!-- <div class="top">
        <ul>
          <li class="active">所有</li>
          <li>待整改</li>
          <li>待复查</li>
          <li>复查未通过</li>
          <li>复查通过</li>
        </ul>
      </div> -->
      <div class="searchBox">
        <ul>
          <li>
            检查结果：
            <el-input v-model="result" placeholder="所有"></el-input>
          </li>
          <li>
            超时状态：
            <el-input v-model="timeStatus" placeholder="所有"></el-input>
          </li>
          <li>
            发起时间：
            <el-date-picker v-model="time" type="date" placeholder="所有"></el-date-picker>
          </li>
          <li>
            &#12288;检查人：
            <el-input v-model="examine" placeholder="所有"></el-input>
          </li>
          <li>
            &#12288;整改人：
            <el-input v-model="repair" placeholder="所有"></el-input>
          </li>
          <li>
            &#12288;复查人：
            <el-input v-model="review" placeholder="所有"></el-input>
          </li>
          <li>
            责任分包：
            <el-select v-model="subpackage" placeholder="所有">
              <el-option
                v-for="item in dutyOptions"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              ></el-option>
            </el-select>
          </li>
          <li>
            检查区域：
            <el-input v-model="area" placeholder="所有"></el-input>
          </li>
          <li>
            隐患类型：
            <el-input v-model="danger" placeholder="所有"></el-input>
          </li>
          <li>
            问题级别：
            <el-input v-model="problem" placeholder="所有"></el-input>
          </li>
          <li></li>
          <li></li>
        </ul>
        <div class="btn">搜索</div>
      </div>
      <div class="tableBox">
        <el-table :data="allTableData" stripe border @row-click="getInfo">
          <el-table-column type="index" label="序号" width="80" :index="indexMethod">
            <!-- <template slot-scope="scope" class="number">
              <div class="number" style="line-height:0.7rem">{{scope.row.number}}</div>
            </template> -->
          </el-table-column>
          <el-table-column prop="problem" label="问题" width="339">
            <template slot-scope="scope">
              <div class="problem">
                <p>{{scope.row.safetyDescribe}}</p>
                <p>
                  <span
                    v-if="scope.row.gradeName=='严重'"
                    class="problemRed problemTu"
                  >{{scope.row.gradeName}}</span>
                  <span
                    v-else-if="scope.row.gradeName=='轻微'"
                    class="problemBlue problemTu"
                  >{{scope.row.gradeName}}</span>
                  <span
                    v-else-if="scope.row.gradeName=='一般'"
                    class="problemYellow problemTu"
                  >{{scope.row.gradeName}}</span>
                  <span v-else class="problemGreen problemTu">{{scope.row.gradeName}}</span>
                  <span style="margin-left:0.05rem">{{scope.row.problemArea}}</span>
                </p>
              </div>
            </template>
          </el-table-column>
          <el-table-column prop="danger" label="隐患类型" width="175">
            <template slot-scope="scope">
              <div class="danger" style="line-height:0.7rem">{{scope.row.hiddenName}}</div>
            </template>
          </el-table-column>
          <el-table-column prop="examine" label="检查人 | 检查时间" width="266">
            <template slot-scope="scope">
              <div class="examine">
                <p>{{scope.row.initiatorName}}</p>
                <p>{{scope.row.initiatorTime}}</p>
              </div>
            </template>
          </el-table-column>
          <el-table-column prop="repair" label="整改人 | 责任分包公司" width="279">
            <template slot-scope="scope">
              <div class="repair">
                <p>{{scope.row.rectifyName}}</p>
                <p>{{scope.row.constructionName}}</p>
              </div>
            </template>
          </el-table-column>
          <el-table-column prop="time" label="整改期限" width="180">
            <template slot-scope="scope">
              <div class="time" style="line-height:0.7rem">{{scope.row.safetyDeadline}}</div>
            </template>
          </el-table-column>
          <el-table-column prop="status" label="状态">
            <template slot-scope="scope">
              <div
                class="status"
                style="line-height:0.7rem;color:#3ada76"
                v-if="scope.row.status==3"
              >已完成</div>
              <div
                class="status"
                style="line-height:0.7rem;color:#feb37f"
                v-else-if="scope.row.status==1"
              >待整改</div>
              <div
                class="status"
                style="line-height:0.7rem;color:#feb37f"
                v-else-if="scope.row.status==2"
              >待复查</div>
              <div
                class="status"
                style="line-height:0.7rem;color:#ff7a81"
                v-else
              >超期未整改</div>
            </template>
          </el-table-column>
        </el-table>
      </div>
      <div class="fenye">
        <!-- 分页的两个事件 -->

        <!-- @size-change="handleSizeChange"
        @current-change="handleCurrentChange"-->
        <el-pagination
          :current-page="pageNum"
          @current-change="handleCurrentChange"
          :page-sizes="[10, 20, 30, 40]"
          :page-size="pageSize"
          layout="total, prev, pager, next, jumper"
          :total="pageTotal"
        ></el-pagination>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      result: "", //检查结果
      timeStatus: "", //超时状态
      time: "", //发起时间
      examine: "", //检查人
      repair: "", //整改人
      review: "", //复查人
      subpackage: "", //责任分包
      area: "", //检查区域
      danger: "", //隐患类型
      problem: "", //问题级别

      dutyOptions: [
        {
          value: "选项1",
          label: "分包公司1"
        },
        {
          value: "选项2",
          label: "分包公司2"
        },
        {
          value: "选项3",
          label: "分包公司3"
        }
      ], //责任分包选项
      allTableData: [], // 表格数据

      pageNum: 1, // 当前页
      pageSize: 8, // 每页显示条数
      pageTotal: 0, // 总条数
      differentiate: 2, // 质量监督
      projectId: '', // 项目id
    };
  },
  created() {
    this.getProjectId()
    this.getInspectionRecordList()
    this.getInformationList()
    // this.getAreaList()
    this.getHiddenList()
  },
  methods: {
    //   行点击事件
    getInfo(row, event, column) {
      this.$router.push(`/systemQuality_recordInfo?id=${row.safetyId}`);
    },

    // 翻页
    handleCurrentChange(val) {
        // console.log(`当前页: ${val}`)
        this.pageNum = val
        this.getInspectionRecordList()
    },

    // 获取项目id
    getProjectId() {
      this.projectId = sessionStorage.getItem('pid')
    },

    // 序号
    indexMethod(index) {
      return (this.pageNum-1)*this.pageSize+index+1
    },

    // 获取检查记录列表
    getInspectionRecordList() {
      this.$axios.post(`http://192.168.1.51:8083/provider/safetyPcApi/getInspectionRecordList?pageNum=${this.pageNum}&pageSize=${this.pageSize}&projectId=${this.projectId}&differentiate=${this.differentiate}`).then(
        res => {
          // console.log(res.data)
          this.allTableData = res.data.data
          this.pageTotal = res.data.total
        }
      )
    },

    // 查询分包单位列表
    getInformationList() {
      this.$axios.post(`http://192.168.1.51:8083/provider/safetyPcApi/getInformationList?projectId=${this.projectId}`).then(
        res => {
          console.log(res.data)
        }
      )
    },

    // 查询检查区域列表
    getAreaList() {
      this.$axios.post(`http://192.168.1.51:8083/provider/safetyPcApi/getAreaList?projectId=${this.projectId}`).then(
        res => {
          console.log(res.data)
        }
      )
    },

    // 查询检查类型列表
    getHiddenList() {
      this.$axios.post(`http://192.168.1.51:8083/provider/safetyPcApi/getHiddenList?projectId=${this.projectId}`).then(
        res => {
          console.log(res.data)
        }
      )
    },
  }
};
</script>

<style lang="less">
#systemQuality_record {
  .content {
    position: relative;
    width: 100%;
    height: 100%;
    background-color: #fff;
    box-shadow: 0 0 0.5rem -0.3rem #666;
    border-radius: 0.04rem;
    .top {
      height: 0.5rem;
      width: 100%;
      position: relative;
      width: 100%;
      font-size: 0.18rem;
      padding-left: 0.2rem;
      border-bottom: 1px solid #f7f7f7;
      ul {
        height: 0.5rem;
        transform: translateX(-0.35rem);
        li {
          cursor: pointer;
          height: 0.5rem;
          margin-left: 0.61rem;
          line-height: 0.5rem;
          float: left;
        }
        li.active {
          color: #0090ff;
          border-bottom: 0.02rem solid #0090ff;
          box-sizing: border-box;
        }
      }
    }
    .searchBox {
      width: 100%;
      height: 2.1rem;
      background-color: #fff;
      position: relative;
      ul {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        padding-left: 0.2rem;
        li {
          margin-top: 0.2rem;
          width: 3.8rem;
          font-size: 0.18rem;
          .el-input {
            width: 2.58rem;
            height: 0.38rem;
          }
          input {
            width: 2.58rem;
            height: 0.38rem;
            border: 0.01rem solid #b6b6b6;
            border-radius: 0.03rem;
          }
        }
      }
      .btn {
        width: 1.61rem;
        height: 0.38rem;
        background-color: #ffd14f;
        border: 0.01rem solid #d4ad40;
        border-radius: 0.03rem;
        color: #fff;
        font-size: 0.2rem;
        text-align: center;
        line-height: 0.38rem;
        position: absolute;
        right: 0.28rem;
        bottom: 0.37rem;
        cursor: pointer;
        &:hover {
          color: #fff;
          background-color: #fcb928;
        }
      }
    }
    .el-table {
      width: 16.38rem;
      th {
        padding: 0;
        div {
          color: #000;
          height: 0.35rem;
          line-height: 0.35rem;
          background-color: #c5e8ff;
          font-size: 0.16rem;
        }
      }
      td {
        padding: 0;
        div {
          height: 0.7rem;
          line-height: .7rem;
          color: #646464;
          font-size: 0.16rem;
          >p {
            line-height: .23rem;
          }
        }
      }
    }
    .tableBox {
      padding: 0 0.2rem;
      .problem {
        // padding-top: 0.12rem;
        .problemTu {
          display: inline-block;
          width: 0.54rem;
          height: 0.19rem;
          border-radius: 0.19rem;
          line-height: 0.19rem;
          color: #fff;
          text-align: center;
          font-size: 0.14rem;
        }
        .problemRed {
          background-color: #ff7a81;
        }
        .problemBlue {
          background-color: #0090ff;
        }
        .problemYellow {
          background-color: #feb37f;
        }
        .problemGreen {
          background-color: #3ada76;
        }
      }
      .examine {
        padding-top: 0.12rem;
      }
      .repair {
        padding-top: 0.12rem;
      }
    }
    .fenye {
      position: absolute;
      right: 0.6rem;
      bottom: 0.3rem;
    }
  }
}
</style>
