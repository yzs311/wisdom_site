<template>
    <div id="systemSchedule_control">
        <div class="content">
            <!-- 按钮栏 -->
            <div class="top-button">
                <div class="button-box">
                    <a class="new" @click="dialogShow=true">
                        <i class="icon"></i>
                        创建节点
                    </a>
                    <a class="contract">
                        <i class="icon"></i>
                        生成计划
                    </a>
                    <a class="derive">
                        <i class="icon"></i>
                        导出计划
                    </a>
                    <a class="cut" @click="ganttShow=!ganttShow">
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
                    <li >
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
                    <li >
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
                        <a class="relevance" @click="relevanceShow=true"></a>
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
                        <a class="relevance" @click="relevanceShow=true"></a>
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
                    </li>
                </ul>
            </div>
            <!-- 关联计划 -->
            <div class="relevance-box" v-show="relevanceShow">
                <!-- 导航栏 -->
                <div class="title">
                    <span>关联计划</span>
                    <a @click="relevanceShow=false">
                        <i class="el-icon-close"></i>
                    </a>
                </div>
                <!-- 按钮栏 -->
                <div class="button-box">
                    <div class="nav-box">
                        <a :class="relevanceActive?'active':''" @click="relevanceActive=true">关联的计划</a>
                        <a :class="!relevanceActive?'active':''" style="margin-left:.38rem;" @click="relevanceActive=false">前置任务</a>
                    </div>
                    <div class="btn-box">
                        <a v-show="relevanceActive">添加进度计划关联</a>
                        <a v-show="!relevanceActive">添加前置任务</a>
                    </div>
                </div>
                <!-- 关联计划列表 -->
                <div class="relevance-list" v-show="relevanceActive">
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
                            <!-- 计划名称 -->
                            <div class="name">
                                计划名称
                            </div>
                            <!-- 计划所占进度 -->
                            <div class="occupation">
                                计划所占进度
                            </div>
                            <!-- 进度 -->
                            <div class="schedule">
                                进度
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
                        </li>
                        <li>
                            <div class="number">
                                1
                            </div>
                            <div class="node">
                                1A、1B电梯工程
                            </div>
                            <div class="name">
                                2019年1月计划
                            </div>
                            <div class="occupation">
                                20%
                            </div>
                            <div class="schedule">
                                <div class="schedule-bar">
                                    <div class="sub-schedule" style="width:50%">50%</div>
                                </div>
                            </div>
                            <div class="plan-start">
                                2018-01-01
                            </div>
                            <div class="plan-end">
                                2018-12-30
                            </div>
                            <div class="practical-start">
                                2018-01-01
                            </div>
                            <div class="practical-end">
                                -
                            </div>
                        </li>
                    </ul>
                    <!-- 分页 -->
                    <div class="paging-box">
                        <!-- @size-change="handleSizeChange"
                            @current-change="handleCurrentChange" -->
                        <el-pagination
                            :current-page="1"
                            :page-size="6"
                            layout="total, prev, pager, next, jumper"
                            :total="1">
                        </el-pagination>
                    </div>
                </div>
                <!-- 前置任务列表 -->
                <div class="preposition-list" v-show="!relevanceActive">
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
                            <!-- 计划名称 -->
                            <div class="name">
                                计划名称
                            </div>
                            <!-- 前置类型 -->
                            <div class="preposition">
                                前置类型
                            </div>
                            <!-- 延迟间隔 -->
                            <div class="interval">
                                延迟间隔
                            </div>
                        </li>
                        <li>
                            <div class="number">
                                1
                            </div>
                            <div class="node">
                                1A、1B电梯工程
                            </div>
                            <div class="name">
                                2019年1月计划
                            </div>
                            <div class="preposition">
                                <input type="text">
                            </div>
                            <div class="interval">
                                <input type="text">
                            </div>
                        </li>
                    </ul>
                    <!-- 分页 -->
                    <div class="paging-box">
                        <!-- @size-change="handleSizeChange"
                            @current-change="handleCurrentChange" -->
                        <el-pagination
                            :current-page="1"
                            :page-size="6"
                            layout="total, prev, pager, next, jumper"
                            :total="1">
                        </el-pagination>
                    </div>
                </div>
            </div>
            <!-- 新增计划节点 -->
            <!-- 新增单位 -->
            <div class="dialog-box" v-show="dialogShow">
                <div class="title">
                    新增计划节点
                    <a class="close" @click="dialogShow=false">
                        <i class="el-icon-close"></i>
                    </a>
                </div>
                <div class="nav">
                    <a @click="newActive=1" :class="newActive==1?'active':''">基础信息</a>
                    <a @click="newActive=2" :class="newActive==2?'active':''">前置任务</a>
                    <a @click="newActive=3" :class="newActive==3?'active':''">关联计划</a>
                </div>
                <div class="form" v-show="newActive==1">
                    <ul>
                        <li>
                            <div>
                                <span>
                                    节点名称
                                    <div class="required">*</div>
                                </span>
                                <input type="text">
                            </div>
                            <div>
                                <span>
                                    父级节点
                                </span>
                                <input type="text">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    计划开始
                                    <div class="required">*</div>
                                </span>
                                <input type="text">
                            </div>
                            <div>
                                <span>
                                    计划结束
                                    <div class="required">*</div>
                                </span>
                                <input type="text">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    实际开始
                                </span>
                                <input type="text">
                            </div>
                            <div>
                                <span>
                                    实际结束
                                </span>
                                <input type="text">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    负责人
                                </span>
                                <input type="text">
                            </div>
                            <div>
                                <span>
                                    分包单位
                                </span>
                                <input type="text">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    流水段
                                </span>
                                <input type="text">
                            </div>
                            <div>
                                <span>
                                    管控级别
                                </span>
                                <input type="text">
                            </div>
                        </li>
                        <li>
                            <div>
                                <span>
                                    工期
                                </span>
                                <input type="text">
                            </div>
                            <div>
                                <span>
                                    关键节点
                                </span>
                                <el-radio v-model="radio" label="1">是</el-radio>
                                <el-radio v-model="radio" label="2">否</el-radio>
                            </div>
                        </li>
                    </ul>
                </div>
                <div class="form" v-show="newActive==2">
                    <div class="button-box">
                        <a>添加</a>
                    </div>
                    <div class="list-box">
                        <ul>
                            <li class="first">
                                <!-- 编号 -->
                                <div class="number">
                                    编号
                                </div>
                                <!-- 任务名称 -->
                                <div class="task-name">
                                    任务名称
                                </div>
                                <!-- 计划名称 -->
                                <div class="plan-name">
                                    计划名称
                                </div>
                                <!-- 前置类型 -->
                                <div class="preposition">
                                    前置类型
                                </div>
                                <!-- 延迟间隔 -->
                                <div class="interval">
                                    延迟间隔
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
                                <div class="task-name">
                                    F1/F2电梯（-3~69F）
                                </div>
                                <div class="plan-name">
                                    2019年11月计划
                                </div>
                                <div class="preposition">
                                    <input type="text">
                                </div>
                                <div class="interval">
                                    <input type="text">
                                </div>
                                <div class="operation">
                                    <i class="el-icon-error"></i>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="form" v-show="newActive==3">
                    <div class="button-box">
                        <a>添加</a>
                    </div>
                    <div class="list-box">
                        <ul>
                            <li class="first">
                                <!-- 编号 -->
                                <div class="number">
                                    编号
                                </div>
                                <!-- 任务名称 -->
                                <div class="task-name">
                                    任务名称
                                </div>
                                <!-- 计划名称 -->
                                <div class="plan-name">
                                    计划名称
                                </div>
                                <!-- 计划所占进度 -->
                                <div class="proportion">
                                    计划所占进度
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
                                <div class="task-name">
                                    F1/F2电梯（-3~69F）
                                </div>
                                <div class="plan-name">
                                    2019年11月计划
                                </div>
                                <div class="proportion">
                                    <input type="text">
                                </div>
                                <div class="operation">
                                    <i class="el-icon-error"></i>
                                </div>
                            </li>
                        </ul>
                    </div>
                </div>
                <div class="confirm">
                    <a class="button">确定</a>
                </div>
            </div>
            <!-- 遮罩层 -->
            <div class="shade-box" v-show="dialogShow"></div>
            <!-- 甘特图 -->
            <div class="gantt-chart" v-show="ganttShow">
                <ul>
                    <li>
                        <!-- 月 -->
                        <div class="month">
                            2019.1
                        </div>
                        <!-- 天 -->
                        <div class="day">
                            <span>1</span>
                            <span>2</span>
                            <span>3</span>
                            <span>4</span>
                            <span>5</span>
                            <span>6</span>
                            <span>7</span>
                            <span>8</span>
                            <span>9</span>
                            <span>10</span>
                            <span>11</span>
                            <span>12</span>
                            <span>13</span>
                            <span>14</span>
                            <span>15</span>
                            <span>16</span>
                            <span>17</span>
                            <span>18</span>
                            <span>19</span>
                            <span>20</span>
                            <span>21</span>
                            <span>22</span>
                            <span>23</span>
                            <span>24</span>
                            <span>25</span>
                            <span>26</span>
                            <span>27</span>
                            <span>28</span>
                            <span>29</span>
                            <span>30</span>
                        </div>
                        <!-- 进度 -->
                        <div class="progress-bar">
                            <div class="schedule-bg" style="width: 100%">
                                <div class="sub-schedule" style="width: 50%">
                                    <div class="text-box">50%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="left:20%;width: 57%">
                                <div class="sub-schedule" style="width: 100%;background-color: #feb37f;">
                                    <div class="text-box">100%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="width: 57%">
                                <div class="sub-schedule" style="width: 80%;background-color: #ff7a81;">
                                    <div class="text-box">80%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="left:10%;width: 67%">
                                <div class="sub-schedule" style="width: 100%">
                                    <div class="text-box">100%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="left:37%;width: 57%">
                                <div class="sub-schedule" style="width: 100%">
                                    <div class="text-box">100%</div>
                                </div>
                            </div>
                        </div>
                    </li>
                    <li>
                        <!-- 月 -->
                        <div class="month">
                            2019.2
                        </div>
                        <!-- 天 -->
                        <div class="day">
                            <span>1</span>
                            <span>2</span>
                            <span>3</span>
                            <span>4</span>
                            <span>5</span>
                            <span>6</span>
                            <span>7</span>
                            <span>8</span>
                            <span>9</span>
                            <span>10</span>
                            <span>11</span>
                            <span>12</span>
                            <span>13</span>
                            <span>14</span>
                            <span>15</span>
                            <span>16</span>
                            <span>17</span>
                            <span>18</span>
                            <span>19</span>
                            <span>20</span>
                            <span>21</span>
                            <span>22</span>
                            <span>23</span>
                            <span>24</span>
                            <span>25</span>
                            <span>26</span>
                            <span>27</span>
                            <span>28</span>
                            <span>29</span>
                            <span>30</span>
                        </div>
                        <!-- 进度 -->
                        <div class="progress-bar">
                            <div class="schedule-bg" style="width: 100%">
                                <div class="sub-schedule" style="width: 50%">
                                    <div class="text-box">50%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="left:20%;width: 57%">
                                <div class="sub-schedule" style="width: 100%;background-color: #feb37f;">
                                    <div class="text-box">100%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="width: 57%">
                                <div class="sub-schedule" style="width: 80%;background-color: #ff7a81;">
                                    <div class="text-box">80%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="left:10%;width: 67%">
                                <div class="sub-schedule" style="width: 100%">
                                    <div class="text-box">100%</div>
                                </div>
                            </div>
                        </div>
                        <div class="progress-bar">
                            <div class="schedule-bg" style="left:37%;width: 57%">
                                <div class="sub-schedule" style="width: 100%">
                                    <div class="text-box">100%</div>
                                </div>
                            </div>
                        </div>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<style lang="less">
    #systemSchedule_control {
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
                ul {
                    padding: .2rem;
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
            .relevance-box {
                width: 17.28rem;
                height: 5.12rem;
                position: fixed;
                left: 1.75rem;
                top: 5.67rem;
                .title {
                    height: .51rem;
                    border-bottom: .01rem  solid #b5b5b5;
                    font-size: .16rem;
                    font-weight: bolder;
                    display: flex;
                    padding: 0 .5rem;
                    line-height: .5rem;
                    justify-content: space-between;
                    background-color: #f2f2f2;
                }
                .button-box {
                    height: .41rem;
                    background-color: #fff;
                    border-bottom: .01rem solid #f3f3f3;
                    display: flex;
                    justify-content: space-between;
                    padding: 0 .5rem;
                    .nav-box {
                        >a {
                            color: #4a4a4a;
                            height: .41rem;
                            font-size: .16rem;
                            line-height: .4rem;
                            display: inline-block;
                            &.active {
                                color: #0090ff;
                                border-bottom: .02rem solid #0090ff;
                            }
                        }
                    }
                    .btn-box {
                        a {
                            width: 1.12rem;
                            display: inline-block;
                            height: .28rem;
                            color: #0090ff;
                            font-size: .12rem;
                            transition: all .5s;
                            line-height: .26rem;
                            border-radius: .02rem;
                            border: .01rem solid #0090ff;
                            text-align: center;
                            transform: translateY(.08rem);
                            &:hover {
                                color: #fff;
                                background-color: #0090ff;
                            }
                        }
                    }
                }
                .relevance-list,
                .preposition-list {
                    height: 4.2rem;
                    background-color: #fff;
                    >ul {
                        padding: .2rem;
                        min-height: 2.1rem;
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
                            .node,
                            .name,
                            .occupation,
                            .interval,
                            .preposition {
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
                                >a {
                                    font-size: .2rem;
                                    text-align: center;
                                }
                            }
                            .relevance {
                                position: absolute;
                                width: .18rem;
                                height: .12rem;
                                background-color: #0090ff;
                                left: .21rem;
                                top: 50%;
                                transform: translateY(-50%);
                            }
                            .preposition,
                            .interval {
                                input {
                                    width: 1.16rem;
                                    height: .28rem;
                                    border: .01rem solid #acabab;
                                    border-radius: .04rem;
                                }
                            }
                        }
                        .first {
                            >div {
                                font-weight: bolder;
                            }
                        }
                    }
                    .paging-box {
                        width: 100%;
                        height: .16rem;
                        margin-top: .2rem;
                        padding-right: .2rem;
                        .el-pagination {
                            float: left;
                            margin-left: 50%;
                            transform: translateX(-50%);
                        }
                    }
                }
            }
            .dialog-box {
                left: 50%;
                top: .22rem;
                z-index: 200;
                width: 12.02rem;
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
                .nav {
                    height: .58rem;
                    border: .01rem solid #dedede;
                    padding: 0 3.28rem;
                    display: flex;
                    justify-content: space-between;
                    >a {
                        color: #4a4a4a;
                        height: .58rem;
                        font-size: .18rem;
                        font-weight: bolder;
                        line-height: .57rem;
                        display: inline-block;
                        &.active {
                            color: #0090ff;
                            border-bottom: .02rem solid #0090ff;
                        }
                    }
                }
                .form {
                    padding-bottom: .3rem;
                    min-height: 4.56rem;
                    >ul{
                        padding-left: .43rem;
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
                    .button-box {
                        height: .49rem;
                        border-bottom: .01rem solid #dedede;
                        padding-top: .1rem;
                        padding-left: .92rem;
                        a {
                            float: left;
                            height: .28rem;
                            width: .98rem;
                            color: #0090ff;
                            font-size: .14rem;
                            transition: all .5s;
                            line-height: .26rem;
                            border-radius: .02rem;
                            border: .01rem solid #0090ff;
                            text-align: center;
                            &:hover {
                                color: #fff;
                                background-color: #0090ff;
                            }
                        }
                    }
                    .list-box {
                        li {
                            padding-left: 1rem;
                            display: flex;
                            height: .61rem;
                            border-bottom: .01rem solid #dedede;
                            >div {
                                color: #4a4a4a;
                                font-size: .14rem;
                                line-height: .6rem;
                                input {
                                    width: 1.35rem;
                                    height: .32rem;
                                    border: .01rem solid #acabab;
                                    border-radius: .04rem;
                                }
                            }
                            .number {
                                width: 1rem;
                            }
                            .task-name,
                            .plan-name {
                                width: 2.3rem;
                            }
                            .preposition,
                            .interval {
                                width: 2rem;
                            }
                            .proportion {
                                width: 4rem;
                            }
                            .operation {
                                font-size: .2rem;
                            }
                        }
                        .first {
                            height: .29rem;
                            background-color: #f8f8f8;
                            >div {
                                color: #4a4a4a;
                                font-size: .16rem;
                                line-height: .28rem;
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
            .gantt-chart {
                width: 11.9rem;
                position: absolute;
                top: .58rem;
                right: .2rem;
                background-color: #fff;
                border-left: .02rem solid #f3f3f3;
                border-right: .01rem solid #f3f3f3;
                min-height: 5.02rem;
                overflow: auto;
                ul {
                    width: 200%;
                    li {
                        float: left;
                        width: 11.87rem;
                        .month {
                            color: #4a4a4a;
                            height: .32rem;
                            font-size: .12rem;
                            font-weight: bolder;
                            border-top: .01rem solid #f3f3f3;
                            border-bottom: .01rem solid #f3f3f3;
                            text-align: center;
                            border-right: .01rem solid #f3f3f3;
                            line-height: .3rem;
                        }
                        .day {
                            color: #4a4a4a;
                            height: .32rem;
                            font-size: .12rem;
                            font-weight: bolder;
                            border-top: .01rem solid #f3f3f3;
                            border-bottom: .01rem solid #f3f3f3;
                            display: flex;
                            justify-content: space-between;
                            span {
                                flex: 1;
                                line-height: .3rem;
                                text-align: center;
                                border-right: .01rem solid #f3f3f3;
                            }
                        }
                        .progress-bar {
                            height: .32rem;
                            border-top: .01rem solid #f3f3f3;
                            border-bottom: .01rem solid #f3f3f3;
                            position: relative;
                            .schedule-bg {
                                height: .12rem;
                                position: absolute;
                                background-color: #e9f2fe;
                                bottom: 0;
                                .sub-schedule {
                                    height: .12rem;
                                    position: relative;
                                    font-size: .12rem;
                                    line-height: .12rem;
                                    background-color: #0090ff;
                                    .text-box {
                                        top: -.14rem;
                                        right: -.24rem;
                                        position: absolute;
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
    }
</style>

<script>
export default {
    data() {
        return {
            relevanceShow: false, // 关联计划显示状态
            relevanceActive: true, // 关联计划当前选中模块
            dialogShow: false, // 对话框状态
            newActive: 1, // 新增对话框当前选中模块
            radio: '1', // 是否关键节点
            ganttShow: false, // 甘特图显示状态
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
        }
    },
}
</script>