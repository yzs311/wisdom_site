<template>
    <div id="systemSchedule_plan">
        <div class="content">
            <!-- 按钮栏 -->
            <div class="top-button">
                <div class="button-box">
                    <a class="new" @click="createShow = true">
                        <i class="icon"></i>
                        创建进度计划
                    </a>
                    <!-- <a class="contract" @click="nodeShow = true">
                        <i class="icon"></i>
                        导入节点
                    </a> -->
                    <a class="derive">
                        <i class="icon"></i>
                        导出计划
                    </a>
                    <a @click="planShow = true">
                        <i class="icon"></i>
                        导入计划
                    </a>
                    <a class="cut">
                        <i class="icon"></i>
                        切换甘特图
                    </a>
                </div>
                <div class="search-box">
                    <el-select v-model="stateValue" placeholder="延迟状态" size="mini" clearable>
                        <el-option
                        v-for="item in stateOptions"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value">
                        </el-option>
                    </el-select>
                    <el-select v-model="rankValue" placeholder="管控级别" size="mini" clearable>
                        <el-option
                        v-for="item in rankOptions"
                        :key="item.value"
                        :label="item.label"
                        :value="item.value"
                        size="mini">
                        </el-option>
                    </el-select>
                    <el-date-picker
                    v-model="dateValue"
                    type="daterange"
                    range-separator="-"
                    start-placeholder="开始日期"
                    end-placeholder="结束日期"
                    size="mini">
                    </el-date-picker>
                </div>
            </div>
            <!-- 主体列表 -->
            <div class="main-list">
                <el-collapse accordion>
                    <el-collapse-item v-for="(item,index) in planList" :key="index">
                        <template slot="title">
                            <span class="name">
                                {{item.name}}（{{item.predictStart.split(' ')[0]}}~{{item.predictEnd.split(' ')[0]}}）
                            </span>
                            <span class="progress-bar">
                                <div class="schedule-bg">
                                    <div class="sub-schedule" style="width: 0%">
                                    </div>
                                </div>
                                <div class="text-box">0%</div>
                            </span>
                            <span class="state">
                                共5个节点，已完成0个，未完成5个
                            </span>
                            <el-dropdown @command="handleCommand">
                                <a class="el-dropdown-link">
                                    <!-- <i class="el-icon-setting"></i> -->
                                </a>
                                <el-dropdown-menu slot="dropdown">
                                    <el-dropdown-item :command="`importNode:${item.id}`">导入节点</el-dropdown-item>
                                    <el-dropdown-item>导出计划</el-dropdown-item>
                                    <el-dropdown-item>导入计划</el-dropdown-item>
                                    <el-dropdown-item :command="`delete:${item.id}`">删除</el-dropdown-item>
                                </el-dropdown-menu>
                            </el-dropdown>
                        </template>
                        <ul>
                            <li class="first">
                                <!-- 编号 -->
                                <div class="number">
                                    编号
                                </div>
                                <!-- 节点 -->
                                <div class="node">
                                    节点
                                </div>
                                <!-- 进度 -->
                                <div class="schedule">
                                    进度
                                </div>
                                <!-- 状态 -->
                                <div class="status">
                                    状态
                                </div>
                                <!-- 级别 -->
                                <div class="rank">
                                    管控级别
                                </div>
                                <!-- 计划工期 -->
                                <div class="plan-time">
                                    计划工期
                                </div>
                                <!-- 实际工期 -->
                                <div class="practical-time">
                                    实际工期
                                </div>
                                <!-- 计划开始 -->
                                <div class="plan-start">
                                    计划开始
                                </div>
                                <!-- 计划结束 -->
                                <div class="plan-end">
                                    计划结束
                                </div>
                                <!-- 实际开始 -->
                                <div class="practical-start">
                                    实际开始
                                </div>
                                <!-- 实际结束 -->
                                <div class="practical-end">
                                    实际结束
                                </div>
                                <!-- 操作 -->
                                <div class="operation">
                                    操作
                                </div>
                            </li>
                            <li>
                                <div class="number">
                                    1
                                </div>
                                <div class="node">
                                    <a>
                                        <i class="el-icon-remove-outline" style="color:#46aeff"></i>
                                    </a>
                                    深圳科伦特产业园中心2019年施工及验收计划
                                    <a>
                                        <i class="el-icon-edit-outline" style="color:#46aeff"></i>
                                    </a>
                                </div>
                                <div class="schedule">
                                    <div class="schedule-bar">
                                        <div class="sub-schedule" style="width:50%">50%</div>
                                    </div>
                                </div>
                                <div class="status">
                                    未开始
                                </div>
                                <div class="rank">
                                    一级
                                </div>
                                <div class="plan-time">
                                    365天
                                </div>
                                <div class="practical-time">
                                    -
                                </div>
                                <div class="plan-start">
                                    2018-01-01
                                </div>
                                <div class="plan-end">
                                    2018-01-25
                                </div>
                                <div class="practical-start">
                                    2018-01-01
                                </div>
                                <div class="practical-end">
                                    -
                                </div>
                                <div class="operation">
                                    <el-dropdown>
                                        <a class="el-dropdown-link">
                                            <i class="el-icon-setting"></i>
                                        </a>
                                        <el-dropdown-menu slot="dropdown">
                                            <el-dropdown-item>插入同级节点</el-dropdown-item>
                                            <el-dropdown-item>插入下级节点</el-dropdown-item>
                                            <el-dropdown-item>编辑</el-dropdown-item>
                                            <el-dropdown-item>删除</el-dropdown-item>
                                        </el-dropdown-menu>
                                    </el-dropdown>
                                </div>
                            </li>
                            <!-- <li >
                                <div class="number">
                                    2
                                </div>
                                <div class="node" style="color:#c0bfbf">
                                    &#12288;&nbsp;开工准备
                                </div>
                                <div class="schedule">
                                    <div class="schedule-bar">
                                        <div class="sub-schedule" style="width:100%">100%</div>
                                    </div>
                                </div>
                                <div class="status" style="color:#3ada76">
                                    正常完成
                                </div>
                                <div class="rank">
                                    一级
                                </div>
                                <div class="plan-time">
                                    365天
                                </div>
                                <div class="practical-time">
                                    -
                                </div>
                                <div class="plan-start">
                                    2018-01-01
                                </div>
                                <div class="plan-end">
                                    2018-01-25
                                </div>
                                <div class="practical-start">
                                    2018-01-01
                                </div>
                                <div class="practical-end">
                                    -
                                </div>
                                <div class="operation">
                                    <el-dropdown>
                                        <a class="el-dropdown-link">
                                            <i class="el-icon-setting"></i>
                                        </a>
                                        <el-dropdown-menu slot="dropdown">
                                            <el-dropdown-item>插入同级节点</el-dropdown-item>
                                            <el-dropdown-item>插入下级节点</el-dropdown-item>
                                            <el-dropdown-item>编辑</el-dropdown-item>
                                            <el-dropdown-item>删除</el-dropdown-item>
                                        </el-dropdown-menu>
                                    </el-dropdown>
                                </div>
                            </li>
                            <li >
                                <div class="number">
                                    3
                                </div>
                                <div class="node">
                                    <a>
                                        <i class="el-icon-circle-plus-outline" style="color:#46aeff"></i>
                                    </a>
                                    主体工程
                                </div>
                                <div class="schedule">
                                    <div class="schedule-bar">
                                        <div class="sub-schedule" style="width:50%">50%</div>
                                    </div>
                                </div>
                                <div class="status" style="color:#feb37f">
                                    超期开始
                                </div>
                                <div class="rank">
                                    三级
                                </div>
                                <div class="plan-time">
                                    24天
                                </div>
                                <div class="practical-time">
                                    -
                                </div>
                                <div class="plan-start">
                                    2018-01-01
                                </div>
                                <div class="plan-end">
                                    2018-01-25
                                </div>
                                <div class="practical-start">
                                    2018-01-01
                                </div>
                                <div class="practical-end">
                                    -
                                </div>
                                <div class="operation">
                                    <el-dropdown>
                                        <a class="el-dropdown-link">
                                            <i class="el-icon-setting"></i>
                                        </a>
                                        <el-dropdown-menu slot="dropdown">
                                            <el-dropdown-item>插入同级节点</el-dropdown-item>
                                            <el-dropdown-item>插入下级节点</el-dropdown-item>
                                            <el-dropdown-item>编辑</el-dropdown-item>
                                            <el-dropdown-item>删除</el-dropdown-item>
                                        </el-dropdown-menu>
                                    </el-dropdown>
                                </div>
                            </li>
                            <li >
                                <a class="relevance"></a>
                                <div class="number">
                                    4
                                </div>
                                <div class="node">
                                    <a>
                                        <i class="el-icon-remove-outline" style="color:#46aeff"></i>
                                    </a>
                                    电梯工程
                                </div>
                                <div class="schedule">
                                    <div class="schedule-bar">
                                        <div class="sub-schedule" style="width:50%">50%</div>
                                    </div>
                                </div>
                                <div class="status" style="color:#ff7a81">
                                    已超期
                                </div>
                                <div class="rank">
                                    三级
                                </div>
                                <div class="plan-time">
                                    24天
                                </div>
                                <div class="practical-time">
                                    -
                                </div>
                                <div class="plan-start">
                                    2018-01-01
                                </div>
                                <div class="plan-end">
                                    2018-01-25
                                </div>
                                <div class="practical-start">
                                    2018-01-01
                                </div>
                                <div class="practical-end">
                                    -
                                </div>
                                <div class="operation">
                                    <el-dropdown>
                                        <a class="el-dropdown-link">
                                            <i class="el-icon-setting"></i>
                                        </a>
                                        <el-dropdown-menu slot="dropdown">
                                            <el-dropdown-item>插入同级节点</el-dropdown-item>
                                            <el-dropdown-item>插入下级节点</el-dropdown-item>
                                            <el-dropdown-item>编辑</el-dropdown-item>
                                            <el-dropdown-item>删除</el-dropdown-item>
                                        </el-dropdown-menu>
                                    </el-dropdown>
                                </div>
                            </li>
                            <li >
                                <a class="relevance"></a>
                                <div class="number">
                                    5
                                </div>
                                <div class="node">
                                    &#12288;&nbsp;1A、1B电梯工程
                                </div>
                                <div class="schedule">
                                    <div class="schedule-bar">
                                        <div class="sub-schedule" style="width:100%">100%</div>
                                    </div>
                                </div>
                                <div class="status" style="color:#ff7a81">
                                    超期完成
                                </div>
                                <div class="rank">
                                    三级
                                </div>
                                <div class="plan-time">
                                    24天
                                </div>
                                <div class="practical-time">
                                    -
                                </div>
                                <div class="plan-start">
                                    2018-01-01
                                </div>
                                <div class="plan-end">
                                    2018-01-25
                                </div>
                                <div class="practical-start">
                                    2018-01-01
                                </div>
                                <div class="practical-end">
                                    -
                                </div>
                                <div class="operation">
                                    <el-dropdown>
                                        <a class="el-dropdown-link">
                                            <i class="el-icon-setting"></i>
                                        </a>
                                        <el-dropdown-menu slot="dropdown">
                                            <el-dropdown-item>插入同级节点</el-dropdown-item>
                                            <el-dropdown-item>插入下级节点</el-dropdown-item>
                                            <el-dropdown-item>编辑</el-dropdown-item>
                                            <el-dropdown-item>删除</el-dropdown-item>
                                        </el-dropdown-menu>
                                    </el-dropdown>
                                </div>
                            </li> -->
                        </ul>
                    </el-collapse-item>
                </el-collapse>
            </div>
            <!-- 新增进度计划 -->
            <div class="dialog-box" v-show="createShow">
                <div class="title">
                    生成计划节点
                    <a class="close" @click="createShow=false">
                        <i class="el-icon-close"></i>
                    </a>
                </div>
                <div class="form">
                    <ul>
                        <li>
                            <span>
                                计划名称
                                <div class="required">*</div>
                            </span>
                            <input type="text" v-model="name">
                        </li>
                        <li>
                            <span>
                                计划时间
                                <div class="required">*</div>
                            </span>
                            <el-date-picker
                            v-model="dateValue"
                            type="daterange"
                            range-separator="至"
                            start-placeholder="开始日期"
                            end-placeholder="结束日期"
                            value-format="yyyy-MM-dd"
                            @change="getTime">
                            </el-date-picker>
                        </li>
                    </ul>
                </div>
                <div class="confirm">
                    <a class="button" @click="addProgressPlan()">确定</a>
                </div>
            </div>
            <!-- 导入节点 -->
            <div class="dialog-box" v-show="nodeShow">
                <div class="title">
                    导入节点
                    <a class="close" @click="nodeShow=false">
                        <i class="el-icon-close"></i>
                    </a>
                </div>
                <!-- <div class="table">
                    <div class="table-title">
                        从总控计划导入
                    </div>
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
                            type="index"
                            label="序号"
                            width="60"
                            :index="indexMethod">
                            </el-table-column>
                            <el-table-column
                            prop="node"
                            label="节点"
                            width="700">
                            </el-table-column>
                            <el-table-column
                            prop="deadline"
                            label="计划工期">
                            </el-table-column>
                            <el-table-column
                            prop="startTime"
                            label="计划开始">
                            </el-table-column>
                            <el-table-column
                            prop="endTime"
                            label="计划结束">
                            </el-table-column>
                            <el-table-column
                            prop="schedule"
                            label="计划所占进度">
                            </el-table-column>
                        </el-table>
                    </div>
                    <div class="paging-box">
                        @current-change="handleCurrentChange2"
                        <el-pagination
                            :current-page="pageNum"
                            layout="total, prev, pager, next, jumper"
                            :total="pageTotal">
                        </el-pagination>
                    </div>
                </div> -->
                <div class="form">
                    <ul>
                        <li>
                            <span>
                                计划名称
                                <div class="required">*</div>
                            </span>
                            <el-select v-model="nodeId" placeholder="请选择">
                                <el-option
                                v-for="item in nodeList"
                                :key="item.id"
                                :label="item.name"
                                :value="item.id">
                                </el-option>
                            </el-select>
                        </li>
                        <li>
                            <span>
                                节点占进度百分比
                                <div class="required">*</div>
                            </span>
                            <input type="text" v-model="progressNodeRatio">
                        </li>
                        <li>
                            <span>
                                进度占节点百分比
                                <div class="required">*</div>
                            </span>
                            <input type="text" v-model="nodeProgressRatio">
                        </li>
                    </ul>
                </div>
                <div class="confirm">
                    <a class="button" @click="addProgressNode()">确定</a>
                </div>
            </div>
            <!-- 导入计划 -->
            <div class="dialog-box" v-show="planShow" style="top:.2rem;width:14.08rem">
                <div class="title">
                    导入计划
                    <a class="close" @click="planShow=false">
                        <i class="el-icon-close"></i>
                    </a>
                </div>
                <div class="table">
                    <div class="table-title">
                        2019年12月计划（2019-12-01~2019-12-30）
                        <a class="click">
                            <i class="icon"></i>
                            点击导入
                        </a>
                    </div>
                    <div class="table-box">
                        <el-table
                        :data="tableData2"
                        stripe
                        border>
                            <el-table-column
                            type="selection"
                            width="35">
                            </el-table-column>
                            <el-table-column
                            type="index"
                            label="序号"
                            width="60"
                            :index="indexMethod2">
                            </el-table-column>
                            <el-table-column
                            prop="name"
                            label="名称"
                            width="500">
                            </el-table-column>
                            <el-table-column
                            prop="change"
                            label="进度变化">
                            </el-table-column>
                            <el-table-column
                            prop="uploading"
                            label="上传人">
                            </el-table-column>
                            <el-table-column
                            prop="date"
                            label="上传日期">
                            </el-table-column>
                            <el-table-column
                            label="操作"
                            width="200">
                            <template>
                                <a style="color:#0090ff">下载</a>
                                <a style="margin-left:.2rem;color:#0090ff">查看备注</a>
                            </template>
                            </el-table-column>
                        </el-table>
                    </div>
                    <div class="paging-box">
                        <!-- @current-change="handleCurrentChange2" -->
                        <el-pagination
                            :current-page="pageNum2"
                            layout="total, prev, pager, next, jumper"
                            :total="pageTotal2">
                        </el-pagination>
                    </div>
                </div>
                <div class="confirm">
                    <a class="button">确定</a>
                </div>
            </div>
            <!-- 遮罩层 -->
            <div class="shade-box" v-show="createShow || nodeShow || planShow"></div>
        </div>
    </div>
</template>

<style lang="less">
    #systemSchedule_plan {
        width: 100%;
        .content {
            border-radius: .04rem;
            background-color: #fff;
            box-shadow: 0 0 .5rem -.3rem #666;
            min-height: 5.6rem;
            position: relative;
            .top-button {
                height: .7rem;
                padding: .2rem;
                display: flex;
                justify-content: space-between;
                .button-box {
                    height: .3rem;
                    a {
                        float: left;
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
                    .new {
                        .icon {
                            background-image: url('../../../../static/images/system-new.png');
                        }
                        &:hover {
                            .icon {
                                background-image: url('../../../../static/images/system-newHover.png');
                            }
                        }
                    }
                    .derive {
                        .icon {
                            background-image: url('../../../../static/images/system-derive.png');
                        }
                        &:hover {
                            .icon {
                                background-image: url('../../../../static/images/system-deriveHover.png');
                            }
                        }
                    }
                    .contract {
                        .icon {
                            background-image: url('../../../../static/images/system-contract.png');
                        }
                        &:hover {
                            .icon {
                                background-image: url('../../../../static/images/system-contractHover.png');
                            }
                        }
                    }
                    .cut {
                        .icon {
                            background-image: url('../../../../static/images/systemGreen-cut.png');
                        }
                        &:hover {
                            .icon {
                                background-image: url('../../../../static/images/systemGreen-cutHover.png');
                            }
                        }
                    }
                }
                .search-box {
                    .el-select {
                        height: .3rem;
                        border: .01rem solid #c0c0c0;
                        border-radius: .04rem;
                        margin-right: .1rem;
                    }
                    .el-date-editor {
                        height: .3rem;
                        border-color: #c0c0c0;
                    }
                }
            }
            .main-list {
                padding: 0 .2rem;
                >.el-collapse {
                    height: .62rem;
                    // border: .01rem solid #f3f3f3;
                    // background-color: #f8f9fb;
                    .el-collapse-item__header {
                        height: .62rem;
                        border: .01rem solid #f3f3f3;
                        background-color: #f8f9fb;
                        display: flex;
                        justify-content: space-between;
                        padding-left: .32rem;
                        .name {
                            width: 7.5rem;
                            color: #4a4a4a;
                            font-size: .16rem;
                        }
                        .progress-bar {
                            height: .6rem;
                            width: 4.1rem;
                            .schedule-bg {
                                width: 2.5rem;
                                height: .15rem;
                                display: inline-block;
                                background-color: #e9f2fe;
                                vertical-align: middle;
                                .sub-schedule {
                                    height: 100%;
                                    background-color: #0090ff;
                                }
                            }
                            .text-box {
                                height: .6rem;
                                color: #4a4a4a;
                                font-size: .16rem;
                                line-height: .6rem;
                                display: inline-block;
                                margin-left: .14rem;
                            }
                        }
                        .state {
                            width: 3.3rem;
                            color: #4a4a4a;
                            font-size: .18rem;
                        }
                        .el-dropdown {
                            height: .62rem;
                            .el-dropdown-link {
                                width: .2rem;
                                height: .62rem;
                                // line-height: .48rem;
                                display: inline-block;
                                background-image: url('../../../../static/images/systemSchedule-icon.png');
                                background-position: center center;
                                background-repeat: no-repeat;
                                background-size: contain;
                            }
                        }
                    }
                    .el-collapse-item__content {
                        padding: 0;
                    }
                }
                ul {
                    // padding: .2rem;
                    li {
                        height: .32rem;
                        width: 100%;
                        padding-left: .52rem;
                        border: .01rem solid #f3f3f3;
                        display: flex;
                        justify-content: space-between;
                        position: relative;
                        >div {
                            color: #4a4a4a;
                            font-size: .12rem;
                            line-height: .3rem;
                        }
                        .schedule {
                            width: .9rem;
                            .schedule-bar {
                                width: .6rem;
                                height: .12rem;
                                background-color: #e9f2fe;
                                transform: translateY(.12rem);
                                .sub-schedule {
                                    background-color: #0090ff;
                                    // width: 50%;
                                    color: #fff;
                                    text-align: center;
                                    height: .12rem;
                                    line-height: .12rem;
                                }
                            }
                        }
                        .number {
                            width: .5rem;
                        }
                        .node {
                            flex: 1;
                        }
                        .status,
                        .rank,
                        .plan-time,
                        .practical-time {
                            width: .7rem;
                        }
                        .plan-start,
                        .plan-end,
                        .practical-start,
                        .practical-end {
                            width: .8rem;
                        }
                        .operation {
                            width: .3rem;
                            a {
                                font-size: .2rem;
                                text-align: center;
                            }
                        }
                        .relevance {
                            position: absolute;
                            width: .18rem;
                            height: .12rem;
                            // background-color: #0090ff;
                            left: .21rem;
                            top: 50%;
                            transform: translateY(-50%);
                            background-image: url('../../../../static/images/systemSchedule-btn.png');
                            background-position: center center;
                            background-repeat: no-repeat;
                            background-size: contain;
                        }
                    }
                    .first {
                        >div {
                            font-weight: bolder;
                        }
                    }
                }
            }
            .dialog-box {
                left: 50%;
                top: 1.5rem;
                z-index: 200;
                width: 6.84rem;
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
                .form {
                    ul{
                        padding-bottom: .3rem;
                        li {
                            display: flex;
                            height: .71rem;
                            padding-top: .3rem;
                            >span {
                                width: 1.85rem;
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
                            }
                            .el-date-editor {
                                width: 3.66rem;
                                height: .41rem;
                                overflow: hidden;
                                input {
                                    padding-left: 0;
                                    border: 0;
                                }
                                span {
                                    width: auto;
                                }
                            }
                        }
                    }
                }
                .table {
                    .table-title {
                        height: .57rem;
                        color: #4a4a4a;
                        font-size: .18rem;
                        text-align: center;
                        line-height: .57rem;
                        font-weight: bolder;
                        position: relative;
                        >a {
                            top: .16rem;
                            right: .4rem;
                            height: .3rem;
                            color: #0090ff;
                            font-size: .14rem;
                            transition: all .5s;
                            line-height: .28rem;
                            border-radius: .02rem;
                            padding-right: .09rem;
                            border: .01rem solid #0090ff;
                            position: absolute;
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
                    >.table-box {
                        width: 100%;
                        min-height: 3.85rem;
                        padding-left: .3rem;
                        padding-right: .3rem;
                        .el-table {
                            width: 16.28rem;
                            // width: 100%;
                            th {
                                padding: 0;
                                div {
                                    color: #4a4a4a;
                                    height: .35rem;
                                    line-height: .35rem;
                                    background-color: #c5e8ff;
                                }
                            }
                            td {
                                padding: 0;
                                div {
                                    height: .35rem;
                                    color: #646464;
                                    line-height: .35rem;
                                }
                            }
                            .table-button {
                                color: #0090ff;
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
                    }
                    >.paging-box {
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
export default {
    data() {
        return {
            stateOptions: [
                {
                    value: 1,
                    label: '提前'
                },
                {
                    value: 2,
                    label: '正常'
                },
                {
                    value: 3,
                    label: '延期'
                }
            ], // 延迟状态选项
            stateValue: '', // 延迟状态值
            rankOptions: [
                {
                    value: 1,
                    label: '一级'
                },
                {
                    value: 2,
                    label: '二级'
                },
                {
                    value: 3,
                    label: '三级'
                }
            ], // 管控级别选项
            rankValue: '', // 管控级别值
            dateValue: '', // 日期
            createShow: false, // 新增对话框显示状态
            nodeShow: false, // 导入节点对话框状态
            planShow: false, // 导入计划对话框状态
            tableData: [
                {
                    node: '深圳科伦特产业园中心2019年施工及验收计划', // 节点
                    deadline: '180天',// 计划工期
                    startTime: '2019-01-01', // 计划开始
                    endTime: '2019-06-01', // 计划结束
                    schedule: '100%', // 计划所占进度
                },
                {
                    node: '深圳科伦特产业园中心2019年施工及验收计划',
                    deadline: '180天',
                    startTime: '2019-01-01',
                    endTime: '2019-06-01',
                    schedule: '100%',
                },
            ], // 导入节点列表数据
            pageSize: 10, // 导入节点每页条数
            pageNum: 1, // 导入节点当前页
            pageTotal: 2, // 导入节点总条数
            tableData2: [
                {
                    name: '2019年12月计划（2019-12-01~2019-12-30）', // 名称
                    change: '10%~90%',// 进度变化
                    uploading: '某某某', // 上传人
                    date: '2019-06-01', // 上传日期
                }
            ], // 导入节点列表数据
            pageSize2: 10, // 导入计划每页条数
            pageNum2: 1, // 导入计划当前页
            pageTotal2: 2, // 导入计划总条数

            creatorId: '', // 创建人id
            nodeList: '', // 节点列表
            planList: '', // 计划列表
            dateValue: '', // 日期范围
            name: '', // 计划名称
            predictStart: '', // 计划开始时间
            predictEnd: '', // 计划结束时间
            nodeId: '', // 节点id
            progressNodeRatio: '', // 节点占进度百分比
            nodeProgressRatio: '', // 进度占节点百分比
            progressId: '', // 当前选中计划id
        }
    },
    created() {
        this.getCreatorId()
        this.selectZhProgressPlanList()
        this.selectZhNodeList()
    },
    methods: {
        // 获取开始时间与结束时间
        getTime() {
            // console.log(this.dateValue)
            this.dateValue?this.predictStart = this.dateValue[0]:this.predictStart=''
            this.dateValue?this.predictEnd = this.dateValue[1]:this.predictEnd=''
        },

        // 操作下拉框点击事件
        handleCommand(command) {
            // console.log(command)
            if (command.split(':')[0] == 'delete') {
                this.remoProgressPlan(command.split(':')[1])
            }
            if (command.split(':')[0] == 'importNode') {
                this.progressId = command.split(':')[1]
                this.nodeShow = true
            }
        },

        // 导入节点序号
        indexMethod(index) {
            return (this.pageNum-1)*this.pageSize+index+1
        },

        // 导入计划序号
        indexMethod2(index) {
            return (this.pageNum-1)*this.pageSize+index+1
        },

        // 获取创建人id
        getCreatorId() {
            this.creatorId = sessionStorage.getItem('userId')
        },

        // 查询节点列表
        selectZhNodeList() {
            this.$axios.post(`http://192.168.1.36:5555/provider/Node/selectZhNodeList?creatorId=${this.creatorId}`).then(
                res => {
                    // console.log(res.data)
                    this.nodeList = res.data.data
                }
            )
        },

        // 获取进度计划列表
        selectZhProgressPlanList() {
            this.$axios.post(`http://192.168.1.36:5555/provider/Node/selectZhProgressPlanList?creatorId=${this.creatorId}`).then(
                res => {
                    // console.log(res.data)
                    this.planList = res.data.data
                    this.selectZhProgressNodeList()
                }
            )
        },

        // 查询计划节点关联列表
        selectZhProgressNodeList() {
            for (let i = 0; i < this.planList.length; i++) {
                // console.log(this.planList[i].id)
                this.$axios.post(`http://192.168.1.36:5555/provider/Node/selectZhProgressNodeList?progressId=${this.planList[i].id}`).then(
                    res => {
                        // console.log(res.data.data)
                        this.planList[i]['nodeList'] = res.data.data
                    }
                )
            }
            // console.log(this.planList)
        },

        // 添加进度计划
        addProgressPlan() {
            this.$axios.post(`http://192.168.1.36:5555/provider/Node/addProgressPlan?name=${this.name}&creatorId=${this.creatorId}&predictStart=${this.predictStart}&predictEnd=${this.predictEnd}`).then(
                res => {
                    // console.log(res.data)
                    if (res.data.code == 0) {
                        this.$message({
                            message: '添加成功',
                            type: 'success'
                        })
                        this.createShow = false
                        this.selectZhProgressPlanList()
                    } else {
                        this.$message({
                            message: '添加失败',
                            type: 'warning'
                        })
                    }
                }
            )
        },

        // 删除进度计划
        remoProgressPlan(id) {
            this.$axios.post(`http://192.168.1.36:5555/provider/Node/remoProgressPlan?id=${id}`).then(
                res => {
                    if (res.data.code == 0) {
                        this.$message({
                            message: '删除成功',
                            type: 'success'
                        })
                        this.selectZhProgressPlanList()
                    } else {
                        this.$message({
                            message: '删除失败',
                            type: 'warning'
                        })
                    }
                }
            )
        },

        // 进度计划导入关联节点
        addProgressNode() {
            this.$axios.post(`http://192.168.1.36:5555/provider/Node/addProgressNode?progressId=${this.progressId}&nodeId=${this.nodeId}&progressNodeRatio=${this.progressNodeRatio}&nodeProgressRatio=${this.nodeProgressRatio}`).then(
                res => {
                    if (res.data.code == 0) {
                        this.$message({
                            message: '导入成功',
                            type: 'success'
                        })
                        this.nodeShow = false
                        this.selectZhProgressPlanList()
                    } else {
                        this.$message({
                            message: '导入失败',
                            type: 'warning'
                        })
                    }
                }
            )
        },

        // 删除进度计划中的关联节点
        removeProgressNode() {
            this.$axios.post(`http://192.168.1.36:5555/provider/Node/removeProgressNode`).then(
                res => {
                    console.log(res.data)
                }
            )
        },
    }
}
</script>