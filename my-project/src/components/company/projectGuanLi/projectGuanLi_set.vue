<template>
    <div id="projectGuanLi_set">
        <div class="centent-box">
            <!-- 搜索栏 -->
            <div class="search-box">
                <div class="input-box">
                    <input type="text" placeholder="请输入项目名称">
                    <a class="el-icon-search"></a>
                </div>
                <a class="new" @click="dialogClick">
                    <i class="icon"></i>
                    新增项目
                </a>
            </div>
            <!-- 列表盒子 -->
            <div class="list-box">
                <!-- 列表 -->
                <div class="table-box">
                    <el-table
                    :data="tableData"
                    stripe
                    border>
                        <el-table-column
                        type="selection"
                        width="35">
                        </el-table-column>
                        <el-table-column
                        prop="number"
                        label="序号"
                        width="60">
                        </el-table-column>
                        <el-table-column
                        prop="project"
                        label="项目名称"
                        width="200">
                        </el-table-column>
                        <el-table-column
                        prop="state"
                        label="状态">
                        <template slot-scope="scope">
                            <div :class="scope.row.state=='运行中'?'green-color':scope.row.state=='待审核'?'yellow-color':'red-color'">
                                {{ scope.row.state }}
                            </div>
                        </template>
                        </el-table-column>
                        <el-table-column
                        label="操作"
                        width="400">
                        <template slot-scope="scope">
                            <a class="table-button">编辑</a>
                            <a class="table-button">移除</a>
                            <a class="table-button">绑定账号</a>
                            <a v-show="scope.row.state=='运行中'" class="table-button">查看秘钥</a>
                            <a v-show="scope.row.state=='运行中'" class="table-button">新增秘钥</a>
                            <a v-show="scope.row.state=='未审核'" class="table-button">提交审核</a>
                            <a v-show="scope.row.state=='审核未通过'" class="table-button">重新审核</a>
                        </template>
                        </el-table-column>
                    </el-table>
                </div>
                <!-- 分页 -->
                <div class="paging-box">
                    <el-pagination
                        @size-change="handleSizeChange"
                        @current-change="handleCurrentChange"
                        :current-page="pageNum"
                        :page-sizes="[10, 20, 30]"
                        :page-size="pageSize"
                        layout="total, sizes, prev, pager, next, jumper"
                        :total="pageTotal">
                    </el-pagination>
                </div>
            </div>
            <!-- 新增对话框 -->
            <div class="dialog-box" v-show="dialogShow">
                <div class="title">
                    新增项目
                    <a class="close" @click="dialogClick">
                        <i class="el-icon-close"></i>
                    </a>
                </div>
                <div class="form1" v-show="dialogPageShow">
                    <ul>
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    项目名称
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="projectName">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    项目简称
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="shortName">
                            </div>
                        </li>
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    项目类型
                                    <span class="required">*</span>
                                </div>
                                <el-select v-model="projectType" placeholder="请选择">
                                    <el-option
                                    v-for="item in typeOptions"
                                    :key="item.value"
                                    :label="item.label"
                                    :value="item.value">
                                    </el-option>
                                </el-select>
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    项目状态
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="projectState">
                            </div>
                        </li>
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    管理人数
                                    <span class="required">*</span>
                                </div>
                                <input type="text">
                            </div>
                            <div class="right-box time">
                                <div class="text-box">
                                    开工时间
                                    <span class="required">*</span>
                                </div>
                                <el-date-picker
                                v-model="startingTime"
                                type="date"
                                placeholder="选择日期">
                                </el-date-picker>
                            </div>
                        </li>
                        <li>
                            <div class="left-box time">
                                <div class="text-box">
                                    合同竣工时间
                                    <span class="required">*</span>
                                </div>
                                <el-date-picker
                                v-model="finishTime"
                                type="date"
                                placeholder="选择日期">
                                </el-date-picker>
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    施工许可证
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="builderLicense">
                            </div>
                        </li>
                        <!-- <li>
                            <div class="left-box">
                                <div class="text-box">
                                    总包单位
                                    <span class="required">*</span>
                                </div>
                                <input type="text">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    监理企业
                                    <span class="required">*</span>
                                </div>
                                <input type="text">
                            </div>
                        </li> -->
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    建筑面积
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="acreage">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    工程造价
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="projectCost">
                            </div>
                        </li>
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    结构类型
                                    <span class="required">*</span>
                                </div>
                                <input type="text">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    负责人
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="projectPrincipal">
                            </div>
                        </li>
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    联系电话
                                    <span class="required">*</span>
                                </div>
                                <input type="text" v-model="phone">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    项目位置
                                    <span class="required">*</span>
                                </div>
                                <el-cascader
                                :options="regionOptions"
                                v-model="selectedRegion"
                                @change="handleChange">
                                </el-cascader>
                            </div>
                        </li>
                        <li>
                            <div class="text-box">
                                详细地址
                                <span class="required">*</span>
                            </div>
                            <input type="text" v-model="projectAddress">
                        </li>
                        <li>
                            <div class="text-box">
                                地图定位
                                <span class="required">*</span>
                            </div>
                            <div class="location-text">你选择的经纬度为：{{longitude}}，{{latitude}}</div>
                        </li>
                        <li class="map-box">
                            <el-amap ref="map" vid="amapDemo" :amap-manager="amapManager" :center="center" :zoom="zoom" :events="events" class="amap-demo">
                            </el-amap>
                        </li>
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    安全报检编号
                                </div>
                                <input type="text" v-model="securityCode">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    质量报检编号
                                </div>
                                <input type="text" v-model="qualityNumber">
                            </div>
                        </li>
                        <!-- <li>
                            <div class="left-box">
                                <div class="text-box">
                                    施工机构代码
                                </div>
                                <input type="text">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    监理机构代码
                                </div>
                                <input type="text">
                            </div>
                        </li> -->
                        <!-- <li>
                            <div class="left-box">
                                <div class="text-box">
                                    监督机构
                                </div>
                                <input type="text">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    建设单位
                                </div>
                                <input type="text">
                            </div>
                        </li> -->
                        <li>
                            <div class="left-box">
                                <div class="text-box">
                                    设计单位
                                </div>
                                <input type="text" v-model="designOrganization">
                            </div>
                            <div class="right-box">
                                <div class="text-box">
                                    勘察单位
                                </div>
                                <input type="text" v-model="explorationUnit">
                            </div>
                        </li>
                        <li>
                            <div class="text-box">
                                备注
                            </div>
                            <input type="text" v-model="remark">
                        </li>
                        <li class="upload-pic">
                            <div class="text-box">
                                项目效果图
                            </div>
                            <a>点击上传</a>
                        </li>
                    </ul>
                </div>
                <div class="form2" v-show="!dialogPageShow">
                    <ul>
                        <li>
                            <div>
                                <span>
                                    单位名称
                                    <div class="required">*</div>
                                </span>
                                <input type="text" v-model="constructionName">
                            </div>
                            <div>
                                <span>
                                    简称
                                    <div class="required">*</div>
                                </span>
                                <input type="text" v-model="shortName">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    社会统一信用代码
                                    <div class="required">*</div>
                                </span>
                                <input type="text" v-model="suid">
                            </div>
                            <div>
                                <span>
                                    法人代表
                                    <div class="required">*</div>
                                </span>
                                <input type="text" v-model="legalPerson">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    单位类型
                                    <div class="required">*</div>
                                </span>
                                <el-select v-model="companyType" placeholder="请选择">
                                    <el-option
                                    v-for="item in contractorType"
                                    :key="item.id"
                                    :label="item.title"
                                    :value="item.id">
                                    </el-option>
                                </el-select>
                            </div>
                            <div>
                                <span>
                                    负责人
                                    <div class="required">*</div>
                                </span>
                                <input type="text" v-model="contacts">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    联系电话
                                    <div class="required">*</div>
                                </span>
                                <input type="number" v-model="mobilePhone">
                            </div>
                            <div>
                                <span>电子邮箱</span>
                                <input type="text" v-model="email">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>开户银行</span>
                                <input type="text" v-model="bankOpen">
                            </div>
                            <div>
                                <span>注册资金</span>
                                <input type="number" v-model="capital">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>开户地址</span>
                                <input type="text" v-model="bankAddress">
                            </div>
                            <div>
                                <span>开户账号</span>
                                <input type="text" v-model="bankNum">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>单位详细地址</span>
                                <input type="text" v-model="address">
                            </div>
                            <div>
                                <span>备注说明</span>
                                <input type="text" v-model="remark">
                            </div>
                        </li>
                    </ul>
                </div>
                <div class="confirm">
                    <a class="button" @click="dialogPageShow=false">下一页</a>
                </div>
            </div>
            <!-- 遮罩层 -->
            <div class="shade-box" v-show="dialogShow"></div>
        </div>
    </div>
</template>

<style lang="less">
    #projectGuanLi_set {
        width: 100%;
        .centent-box {
            border-radius: .04rem;
            background-color: #fff;
            box-shadow: 0 0 .5rem -.3rem #666;
            .search-box {
                height: .7rem;
                padding-top: .15rem;
                padding-left: .2rem;
                .input-box {
                    width: 4rem;
                    height: .4rem;
                    overflow: hidden;
                    padding-left: .16rem;
                    border-radius: .04rem;
                    display: inline-block;
                    border: .01rem solid #b6b6b6;
                    input {
                        width: 3.4rem;
                        height: .38rem;
                        font-size: .17rem;
                        &::placeholder {
                            color: #dadada;
                        }
                    }
                    a {
                        color: #ccc;
                        width: .38rem;
                        height: .38rem;
                        font-size: .18rem;
                        text-align: center;
                        line-height: .38rem;
                        transition: all .5s;
                        display: inline-block;
                        &:hover {
                            color: #fff;
                            background-color: #ccc;
                        }
                    }
                }
                .new {
                    float: right;
                    height: .3rem;
                    color: #0090ff;
                    font-size: .14rem;
                    transition: all .5s;
                    margin-right: .2rem;
                    line-height: .28rem;
                    border-radius: .02rem;
                    padding-right: .09rem;
                    border: .01rem solid #0090ff;
                    &:hover {
                        color: #fff;
                        background-color: #0090ff;
                    }
                    .icon {
                        width: .37rem;
                        height: .28rem;
                        transition: all .5s;
                        display: inline-block;
                        vertical-align: middle;
                        background-repeat: no-repeat;
                        background-position: center center;
                    }
                }
            }
            .list-box {
                .table-box {
                    width: 100%;
                    min-height: 6.6rem;
                    padding-left: .2rem;
                    .el-table {
                        width: 16.28rem;
                        // width: 100%;
                        th {
                            padding: 0;
                            div {
                                color: #4a4a4a;
                                height: .6rem;
                                line-height: .6rem;
                                background-color: #c5e8ff;
                            }
                        }
                        td {
                            padding: 0;
                            div {
                                height: .6rem;
                                color: #646464;
                                line-height: .6rem;
                            }
                        }
                        .table-button {
                            color: #2323ff;
                            padding: 0 .08rem;
                            text-decoration: underline;
                        }
                    }
                    .green-color {
                        color: #58de87 !important;
                    }
                    .red-color {
                        color: #fe898f !important;
                    }
                    .yellow-color {
                        color: #f5c98d !important;
                    }
                }
                .paging-box {
                    width: 100%;
                    height: .52rem;
                    margin-top: .2rem;
                    padding-right: .2rem;
                    padding-bottom: .2rem;
                    .el-pagination {
                        float: right;
                    }
                }
            }
            .dialog-box {
                left: 50%;
                top: .48rem;
                z-index: 200;
                width: 12.15rem;
                // height: 7rem;
                overflow: hidden;
                position: absolute;
                border-radius: .1rem;
                transform: translate(-50%);
                background-color: #fefefe;
                .title {
                    color:#fff;
                    height: .6rem;
                    font-size: .24rem;
                    line-height: .6rem;
                    text-align: center;
                    position: relative;
                    font-weight: bolder;
                    background: linear-gradient(to right, #6cc4ff, #489cff);
                    a {
                        top: 50%;
                        right: .2rem;
                        color: #fff;
                        position: absolute;
                        transform: translateY(-50%);
                    }
                }
                .form1 {
                    overflow: auto;
                    height: 5.6rem;
                    // ul{
                    //     padding-bottom: .35rem;
                    //     li {
                    //         display: flex;
                    //         height: .85rem;
                    //         padding-top: .35rem;
                    //         >span {
                    //             width: 2.64rem;
                    //             height: .5rem;
                    //             font-size: .16rem;
                    //             text-align: right;
                    //             position: relative;
                    //             line-height: .5rem;
                    //             padding-right: .32rem;
                    //             display: inline-block;
                    //             .required {
                    //                 top: -0.01rem;
                    //                 right: .22rem;
                    //                 color: #f00;
                    //                 position: absolute;
                    //             }
                    //         }
                    //         input {
                    //             width: 6rem;
                    //             height: .5rem;
                    //             padding-left: .1rem;
                    //             border-radius: .04rem;
                    //             border: .01rem solid #b1b1b1;
                    //             &::-webkit-outer-spin-button,
                    //             &::-webkit-inner-spin-button {
                    //                 appearance: none;
                    //             }
                    //             &[type="number"] {
                    //                 appearance: textfield;
                    //             }
                    //         }
                    //     }
                    // }
                    ul {
                        padding-top: .26rem;
                        li {
                            height: .4rem;
                            padding-left: .5rem;
                            margin-bottom: .3rem;
                            .left-box {
                                float: left;
                                width: 5.38rem;
                                .text-box {
                                    width: 1.7rem;
                                    color: #4a4a4a;
                                    font-size: .16rem;
                                    text-align: right;
                                    line-height: .4rem;
                                    padding-right: .3rem;
                                    display: inline-block;
                                    .required {
                                        color: #f00;
                                    }
                                }
                                input {
                                    width: 3.68rem;
                                    height: .4rem;
                                    padding-left: .1rem;
                                    border-radius: .05rem;
                                    border: .01rem solid #acabab;
                                }
                            }
                            .right-box {
                                float: left;
                                width: 5.38rem;
                                .text-box {
                                    width: 1.7rem;
                                    color: #4a4a4a;
                                    font-size: .16rem;
                                    text-align: right;
                                    line-height: .4rem;
                                    padding-right: .3rem;
                                    display: inline-block;
                                    .required {
                                        color: #f00;
                                    }
                                }
                                input {
                                    width: 3.68rem;
                                    height: .4rem;
                                    padding-left: .1rem;
                                    border-radius: .05rem;
                                    border: .01rem solid #acabab;
                                }
                            }
                            .text-box {
                                width: 1.7rem;
                                color: #4a4a4a;
                                font-size: .16rem;
                                text-align: right;
                                line-height: .4rem;
                                padding-right: .3rem;
                                display: inline-block;
                                .required {
                                    color: #f00;
                                }
                            }
                            input {
                                width: 9.09rem;
                                height: .4rem;
                                padding-left: .1rem;
                                border-radius: .05rem;
                                border: .01rem solid #acabab;
                            }
                            .location-text {
                                font-size: .16rem;
                                display: inline-block;
                            }
                            .time {
                                .el-input__icon {
                                    display: none;
                                }
                            }
                        }
                        .map-box {
                            padding: 0;
                            width: 9.08rem;
                            height: 5.32rem;
                            margin-left: 2.2rem;
                        }
                        .upload-pic {
                            height: 1.31rem;
                            a {
                                width: 1.31rem;
                                height: 1.31rem;
                                color: #acabab;
                                font-size: .18rem;
                                text-align: center;
                                line-height: 1.31rem;
                                display: inline-block;
                                background-image: url('../../../../static/images/imaginary-line.png');
                                background-position: center center;
                                background-repeat: no-repeat;
                                background-size: contain;
                            }
                        }
                    }
                }
                .form2 {
                    padding-left: .43rem;
                    padding-bottom: .3rem;
                    ul{
                        li {
                            display: flex;
                            height: .71rem;
                            padding-top: .3rem;
                            >div {
                                width: 5.38rem;
                                >span {
                                    width: 1.72rem;
                                    height: .41rem;
                                    font-size: .16rem;
                                    text-align: right;
                                    position: relative;
                                    line-height: .41rem;
                                    padding-right: .32rem;
                                    display: inline-block;
                                    .required {
                                        top: -0.01rem;
                                        right: .22rem;
                                        color: #f00;
                                        position: absolute;
                                    }
                                }
                                input {
                                    width: 3.66rem;
                                    height: .41rem;
                                    padding-left: .1rem;
                                    border-radius: .02rem;
                                    border: .01rem solid #b1b1b1;
                                    &::-webkit-outer-spin-button,
                                    &::-webkit-inner-spin-button {
                                        appearance: none;
                                    }
                                    &[type="number"] {
                                        appearance: textfield;
                                    }
                                }
                                .el-date-editor {
                                    width: 3.66rem;
                                    height: .41rem;
                                    input {
                                        padding-left: .3rem;
                                    }
                                }
                            }
                        }
                    }
                }
                .confirm {
                    height: .8rem;
                    background-color: #f8f8f8;
                    border-top: .01rem solid #dedede;
                    .button {
                        color: #fff;
                        display: block;
                        width: 1.63rem;
                        height: .49rem;
                        margin: 0 auto;
                        font-size: .2rem;
                        margin-top: .15rem;
                        text-align: center;
                        line-height: .47rem;
                        transition: all .5s;
                        border-radius: .02rem;
                        background-color: #ffd14f;
                        border: .01rem solid #d9b759;
                        &:hover {
                            background-color: #d9b759
                        }
                    }
                }
            }
            .shade-box {
                top: 0;
                left: 0;
                width: 100%;
                z-index: 100;
                height: 100%;
                position: fixed;
                background-color: rgba(0, 0, 0, .5);
            }
        }
    }
</style>

<script>
let amapManager = new VueAMap.AMapManager()
export default {
    data() {
        return {
            tableData: [{
                number: 1, // 序号
                project: '深圳市某某某项目', // 项目名称
                state: '待审核', // 状态
            },{
                number: 2, // 序号
                project: '深圳市某某某项目', // 项目名称
                state: '运行中', // 状态
            },{
                number: 2, // 序号
                project: '深圳市某某某项目', // 项目名称
                state: '未审核', // 状态
            },{
                number: 2, // 序号
                project: '深圳市某某某项目', // 项目名称
                state: '审核未通过', // 状态
            }], // 表格数据
            pageNum: 1, // 当前页码
            pageSize: 10, // 每页显示条数
            pageTotal: 0, // 总条数
            dialogShow: false, // 对话框显示状态
            dialogPageShow: true, // 当前对话框的页数
            amapManager,
            zoom: 12,
            center: [114.014129,22.571492],
            events: {
                init: (o) => {
                },
                'moveend': () => {
                },
                'zoomchange': () => {
                },
                'click': (e) => {
                    // console.log(e.lnglat)
                    this.longitude = e.lnglat.lng
                    this.latitude = e.lnglat.lat
                    // console.log(this.longitude+':'+this.latitude)
                }
            },
            longitude: '', // 经度
            latitude: '', // 纬度
            typeOptions: [{
                value: '选项1',
                label: '类型1'
            }, {
                value: '选项2',
                label: '类型2'
            }, {
                value: '选项3',
                label: '类型3'
            }, {
                value: '选项4',
                label: '类型4'
            }, {
                value: '选项5',
                label: '类型5'
            }], // 项目类别选项
            type: '', // 项目类别当前选中
            startWorkTime: '', // 开工时间
            completedTime: '', // 竣工时间
            regionOptions: [{
                value: '广东省',
                label: '广东省',
                children: [{
                    value: '深圳市',
                    label: '深圳市',
                    children: [{
                        value: '罗湖区',
                        label: '罗湖区'
                    },{
                        value: '南山区',
                        label: '南山区'
                    },{
                        value: '福田区',
                        label: '福田区'
                    },{
                        value: '龙岗区',
                        label: '龙岗区'
                    },{
                        value: '龙华区',
                        label: '龙华区'
                    },{
                        value: '宝安区',
                        label: '宝安区'
                    }]
                }]
            }], // 地区列表

            // 对话框数据
            selectedRegion: [], // 当前选中地区
            cid: '', // 所属公司id
            projectName: '', // 项目名称
            shortName: '', // 简称
            projectPrincipal: '', // 项目负责人
            phone: '', // 联系方式
            projectType: '', // 项目类型 
            projectState: '', // 项目状态 
            projectNumber: '', // 项目管理人数
            projectRegion: '', // 所属地区
            builderLicense: '', // 	施工许可证
            projectAddress: '', // 项目地址
            startingTime: '', // 起始时间
            finishTime: '', // 结束时间
            acreage: '', // 建筑面积
            projectCost: '', // 工程造价
            longitude: '', // 经度
            latitude: '', // 纬度
            securityCode: '', // 安全报监编号
            qualityNumber: '', // 质量报监编号
            designOrganization: '', // 设计单位
            explorationUnit: '', // 勘察单位
            remark: '', // 	备注
            projectImage: '', // 项目效果图
            // 建立单位参数
            contractorType: [], // 单位类型选项
            constructionName: '', // 参建单位名称
            shortName: '', // 简称
            capital: '', // 注册资金
            companyType: '', // 单位类型 
            legalPerson: '', // 法人代表
            suid: '', // 社会统一信用代码
            organizationCode: '', // 组织机构代码
            bankOpen: '', // 开户银行
            bankNum: '', // 开户账号
            bankAddress: '', // 开户地址
            address: '', // 单位详细地址
            contacts: '', // 负责人
            mobilePhone: '', // 电话
            email: '', // 电子邮箱
            remark: '', // 备注
        }
    },
    created() {
        this.getArea()
        this.selectProjectList()
    },
    methods: {
        // 每页条数切换
        handleSizeChange(val) {
            // console.log(`每页 ${val} 条`)
            this.pageSize = val
            // this.selectConstructionCompanyList()
        },

        // 当前页
        handleCurrentChange(val) {
            // console.log(`当前页: ${val}`)
            this.pageNum = val
            // this.selectConstructionCompanyList()
        },

        // 新增对话框状态切换
        dialogClick() {
            this.dialogShow = !this.dialogShow
        },

        // 地区选择框监听事件
        handleChange(value) {
            console.log(value)
        },

        // 获取城市数据
        getArea() {
            this.$axios.post(`/api/area/getArea?parentId=0`).then(
                res => {
                    // console.log(res.data)
                    let temp = []
                    for (let i = 0; i < res.data.data.length; i++) {
                        this.$axios.post(`/api/area/getArea?parentId=${res.data.data[i].id}`).then(
                            res2 => {
                                // console.log(res2.data.data)
                                let temp2 = []
                                for (let i2 = 0; i2 < res2.data.data.length; i2++) {
                                    this.$axios.post(`/api/area/getArea?parentId=${res2.data.data[i2].id}`).then(
                                        res3 => {
                                            // console.log(res3.data)
                                            // if (res3.data) {
                                                let temp3 = []
                                                for (let i3 = 0; i3 < res3.data.data.length; i3++) {
                                                    temp3.push({
                                                        value: res3.data.data[i3].id,
                                                        label: res3.data.data[i3].title
                                                    })
                                                }
                                                temp2.push({
                                                    value: res2.data.data[i2].id,
                                                    label: res2.data.data[i2].title,
                                                    children: temp3
                                                })
                                            // }
                                        }
                                    )
                                }
                                temp.push({
                                    value: res.data.data[i].id,
                                    label: res.data.data[i].title,
                                    children: temp2
                                })
                            }
                        )
                    }
                    this.regionOptions = temp
                    console.log(temp)
                }
            )
        },

        // 获取项目列表
        selectProjectList() {
            this.$axios.post(`/api/project/selectProjectList?cid=1&pageNum=${this.pageNum}&pageSize=${this.pageSize}`).then(
                res => {
                    console.log(res.data)
                }
            )
        }
    }
}
</script>