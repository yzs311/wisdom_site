<template>
  <div id="systemQuality_manageInfo">
    <div class="content">
      <div class="tab">
        <span @click="$router.push('/systemQuality_manage')">
          <i class="el-icon-arrow-left" style="font-size:0.18rem"></i>
          返回&nbsp;/&nbsp;
        </span>
        <!-- <span @click="$router.push('/systemQuality_home')">数据统计&nbsp;/&nbsp;</span> -->
        <span @click="$router.push('/systemQuality_manage')">整改单管理&nbsp;/&nbsp;</span>
        <span>详情</span>
      </div>
      <div class="status">
        <div class="box">
          <p class="text">{{indexData.status==1?'待整改':indexData.status==2?'待复查':indexData.status==3?'已完成':'超期未整改'}}</p>
          <p class="time">整改时间：{{indexData.safetyDeadline}}</p>
        </div>
      </div>
      <div class="tableBox">
        <div class="title">
          <span class="shu"></span>
          <span class="text">隐患明细</span>
        </div>
        <el-table :data="allTableData" stripe border>
          <el-table-column prop="problem" label="问题">
            <template slot-scope="scope">
              <div class="problem">
                <p>{{indexData.safetyDescribe}}</p>
                <p style="height:.23rem;overflow:hidden;">
                  <span
                    v-if="indexData.gradeName=='严重'"
                    class="problemRed problemTu"
                  >{{indexData.gradeName}}</span>
                  <span
                    v-else-if="indexData.gradeName=='轻微'"
                    class="problemBlue problemTu"
                  >{{indexData.gradeName}}</span>
                  <span
                    v-else-if="indexData.gradeName=='一般'"
                    class="problemYellow problemTu"
                  >{{indexData.gradeName}}</span>
                  <span v-else class="problemGreen problemTu">{{indexData.gradeName}}</span>
                  <span style="margin-left:0.05rem">{{indexData.areaName}}</span>
                </p>
              </div>
            </template>
          </el-table-column>
          <el-table-column prop="danger" label="隐患类型" width="185">
            <template slot-scope="scope">
              <div class="danger" style="line-height:0.7rem">{{indexData.hiddenName}}</div>
            </template>
          </el-table-column>
          <el-table-column prop="examine" label="检查人 | 检查时间" width="275">
            <template slot-scope="scope">
              <div class="examine">
                <p>{{indexData.initiatorName}}</p>
                <p>{{indexData.initiatorTime}}</p>
              </div>
            </template>
          </el-table-column>
          <el-table-column prop="repair" label="整改人 | 责任分包公司" width="295">
            <template slot-scope="scope">
              <div class="repair">
                <p>{{indexData.rectifyName}}</p>
                <p>{{indexData.constructionName}}</p>
              </div>
            </template>
          </el-table-column>
          <el-table-column prop="time" label="整改期限" width="195">
            <template slot-scope="scope">
              <div class="time" style="line-height:0.7rem">{{indexData.safetyDeadline}}</div>
            </template>
          </el-table-column>
          <el-table-column prop="status" label="状态" width="185">
            <template slot-scope="scope">
              <div
                style="line-height:0.7rem;color:#3ada76"
                v-if="scope.row.status== 3"
              >已完成</div>
              <div
                style="line-height:0.7rem;color:#feb37f"
                v-else-if="scope.row.status==1"
              >待整改</div>
              <div
                style="line-height:0.7rem;color:#feb37f"
                v-else-if="scope.row.status==2"
              >待复查</div>
              <div style="line-height:0.7rem;color:#ff7a81" v-else>超期未整改</div>
            </template>
          </el-table-column>
          <!-- <el-table-column label="操作">
            <template slot-scope="scope">
              <div style="line-height:0.7rem">
                <a @click="handleDelete(scope.row)">删除</a>
              </div>
            </template>
          </el-table-column> -->
        </el-table>
      </div>
      <div class="searchBox">
        <div class="title">
          <span class="shu"></span>
          <span class="text">整改单基础信息</span>
        </div>

        <ul>
          <li>
            &#12288;检查人：
            <el-input v-model="jianChaPerson" placeholder="所有"></el-input>
          </li>
          <li>
            &#12288;整改人：
            <el-input v-model="zhengGaiPerson" placeholder="所有"></el-input>
          </li>
          <li>
            &#12288;复查人：
            <el-input v-model="fuChaPerson" placeholder="所有"></el-input>
          </li>
          <li>
            &#12288;参与人：
            <el-input v-model="fuChaPerson" placeholder="所有"></el-input>
          </li>
          <li>
            检查日期：
            <el-date-picker v-model="value1" type="date" placeholder="所有"></el-date-picker>
          </li>

          <li>
            整改日期：
            <el-date-picker v-model="value1" type="date" placeholder="所有"></el-date-picker>
          </li>
          <li>
            检查区域：
            <el-input v-model="fuChaPerson" placeholder="所有"></el-input>
          </li>
          <li>
            复查日期：
            <el-date-picker v-model="value1" type="date" placeholder="所有"></el-date-picker>
          </li>

          <li>
            整改期限：
            <el-date-picker v-model="value1" type="date" placeholder="所有"></el-date-picker>
          </li>
          <li>
            检查类型：
            <el-input v-model="fuChaPerson" placeholder="所有"></el-input>
          </li>
          <li></li>
          <li></li>
        </ul>
        <div class="li">
          整改要求：
          <el-input type="textarea" :rows="4" placeholder="请输入内容" v-model="textarea"></el-input>
        </div>
      </div>
      <div class="btn">确定</div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      allTableData: [
        {
          number: 1,
          problem: "某某某工地没护栏",
          problemStatus: "严重",
          problemArea: "南山EPC创新工业园",
          danger: "施工用电",
          examine: "某某某",
          examineTime: "2019-01-01 20:11",
          repair: "伟业-某某某",
          repairSubpackage: "深圳市伟业建筑劳务有限公司",
          time: "2018-01-23",
          status: "复查通过"
        }
      ],

      safetyId: '', // 整改id
      getIdState: 0, // 调用一次获取url中的值
      indexData: '', // 页面数据
    }
  },
  created() {
    this.getSafetyId()
    this.getManagementDetails()
  },
  methods: {
    // 获取实时监控页面传过来的值
    getSafetyId() {
        if (this.$route.query.id != undefined && this.getIdState == 0) {
            this.safetyId = this.$route.query.id
            this.getIdState = 1
        }
        // console.log(this.safetyId)
    },

    // 获取整改单管理详情
    getManagementDetails() {
      this.$axios.post(`http://192.168.1.51:8083/provider/safetyPcApi/getManagementDetails?safetyId=${this.safetyId}`).then(
        res => {
          // console.log(res.data)
          this.indexData = res.data.data
        }
      )
    }
  }
};
</script>
<style lang="less">
#systemQuality_manageInfo {
  .content {
    position: relative;
    width: 100%;
    height: 100%;
    background-color: #fff;
    box-shadow: 0 0 0.5rem -0.3rem #666;
    border-radius: 0.04rem;
    padding: 0.17rem 0.2rem 0.4rem 0.2rem;
    .tab {
      span {
        display: inline-block;
        height: 0.3rem;
        cursor: pointer;
        font-size: 0.16rem;
        line-height: 0.3rem;
      }
    }
    .status {
      margin-top: 0.2rem;
      height: 0.95rem;
      width: 100%;
      background-color: #f2f9ff;
      padding-top: 0.25rem;
      padding-left: 0.33rem;
      .text {
        font-size: 0.18rem;
        color: #3ea0ff;
        font-weight: 600;
      }
      .time {
        color: #4a4a4a;
        margin-top: 0.03rem;
        font-size: 0.16rem;
      }
    }
    .el-table {
      margin-top: 0.2rem;
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
          color: #646464;
          font-size: 0.16rem;
        }
      }
    }
    .tableBox {
      margin-top: 0.35rem;
      .problem {
        padding-top: 0.12rem;
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
        .a {
          line-height: 0.7rem;
        }
      }
      .examine {
        padding-top: 0.12rem;
      }
      .repair {
        padding-top: 0.12rem;
      }
    }
    .title {
      font-size: 0.18rem;
      font-weight: 600;
      .shu {
        display: inline-block;
        width: 0.04rem;
        height: 0.18rem;
        background-color: #0090ff;
        transform: translateY(0.04rem);
      }
      .text {
        margin-left: 0.16rem;
      }
    }
    .searchBox {
      margin-top: 0.4rem;
      width: 100%;
      //   height: 1.4rem;
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
      .li {
        margin-top: 0.2rem;
        width: 3.8rem;
        font-size: 0.18rem;
        margin-left: 0.2rem;
        width: 7.87rem;
        .el-textarea__inner {
          width: 6.83rem;
          transform: translate(0.94rem, -0.25rem);
          border: 0.01rem solid #b6b6b6;
        }
      }
    }
    .btn {
      width: 1.61rem;
      height: 0.47rem;
      background-color: #ffd14f;
      border: 0.01rem solid #d4ad40;
      border-radius: 0.03rem;
      color: #fff;
      font-size: 0.2rem;
      text-align: center;
      line-height: 0.47rem;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      bottom: 1rem;
      cursor: pointer;
      &:hover {
        color: #fff;
        background-color: #fcb928;
      }
    }
  }
}
</style>

