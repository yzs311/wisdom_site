<template>
    <div id="companyGuanLi_user">
        <div class="centent-box">
            <!-- 搜索栏 -->
            <div class="search-box">
                <div class="input-box">
                    <input type="text" placeholder="请输入账号或姓名">
                    <a class="el-icon-search"></a>
                </div>
                <div class="input-box" style="margin-left:.5rem">
                    <input type="text" placeholder="请输入公司名称">
                    <a class="el-icon-search"></a>
                </div>
                <a class="new" @click="dialogClick">
                    <i class="icon"></i>
                    新增用户
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
                        prop="account"
                        label="账号"
                        width="150">
                        </el-table-column>
                        <el-table-column
                        prop="name"
                        label="姓名"
                        width="100">
                        </el-table-column>
                        <el-table-column
                        prop="company"
                        label="所属公司"
                        width="200">
                        </el-table-column>
                        <el-table-column
                        prop="role"
                        label="公司角色"
                        width="150">
                        </el-table-column>
                        <el-table-column
                        prop="state"
                        label="状态">
                        <template slot-scope="scope">
                            <div :class="scope.row.state=='有效'?'green-color':'red-color'">
                                {{ scope.row.state }}
                            </div>
                        </template>
                        </el-table-column>
                        <el-table-column
                        label="操作"
                        width="200">
                        <template>
                            <a class="table-button">编辑</a>
                            <a class="table-button">删除</a>
                        </template>
                        </el-table-column>
                    </el-table>
                </div>
                <!-- 分页 -->
                <div class="paging-box">
                    <el-pagination
                        @size-change="handleSizeChange"
                        @current-change="handleCurrentChange"
                        :current-page="page"
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
                    新增公司
                    <a class="close" @click="dialogClick">
                        <i class="el-icon-close"></i>
                    </a>
                </div>
                <div class="form">
                    <ul>
                        <li>
                            <span>
                                姓名
                                <div class="required">*</div>
                            </span>
                            <input type="text" v-model="userName">
                        </li>
                        <li>
                            <span>
                                手机号
                                <div class="required">*</div>
                            </span>
                            <input type="number" onkeypress="return (/[\d]/.test(String.fromCharCode(event.keyCode)))" v-model="userPhone">
                        </li>
                        <li>
                            <span>
                                账号
                                <div class="required">*</div>
                            </span>
                            <input type="text" v-model="userAccount" @blur="selectSystemUser">
                        </li>
                        <li>
                            <span>
                                密码
                                <div class="required">*</div>
                            </span>
                            <input type="text" v-model="userPassword">
                        </li>
                        <li>
                            <span>
                                账户状态
                                <div class="required">*</div>
                            </span>
                            <el-select v-model="userState" placeholder="请选择">
                                <el-option
                                v-for="item in userStateOptions"
                                :key="item.value"
                                :label="item.label"
                                :value="item.value">
                                </el-option>
                            </el-select>
                        </li>
                        <li>
                            <span>
                                登录项
                                <div class="required">*</div>
                            </span>
                            <el-select v-model="entry" placeholder="请选择">
                                <el-option
                                v-for="item in entryOptions"
                                :key="item.value"
                                :label="item.label"
                                :value="item.value">
                                </el-option>
                            </el-select>
                        </li>
                    </ul>
                </div>
                <div class="confirm">
                    <a class="button" @click="querySystemUser">确定</a>
                </div>
            </div>
            <!-- 遮罩层 -->
            <div class="shade-box" v-show="dialogShow"></div>
        </div>
    </div>
</template>

<style lang="less">
    #companyGuanLi_user {
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
                top: 1.6rem;
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
                    overflow: auto;
                    ul{
                        padding-bottom: .3rem;
                        li {
                            display: flex;
                            height: .7rem;
                            padding-top: .3rem;
                            >span {
                                width: 1.15rem;
                                height: .4rem;
                                font-size: .16rem;
                                text-align: right;
                                position: relative;
                                line-height: .4rem;
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
                                width: 5.4rem;
                                height: .4rem;
                                padding-left: .1rem;
                                border-radius: .04rem;
                                border: .01rem solid #b1b1b1;
                                &::-webkit-outer-spin-button,
                                &::-webkit-inner-spin-button {
                                    appearance: none;
                                }
                                &[type="number"] {
                                    appearance: textfield;
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
export default {
    data() {
        return  {
            tableData: [{
                number: 1, // 序号
                account: 'admin', // 账号
                name: '某某某', // 姓名
                company: '深圳市市政工程有限公司', // 所属公司
                role: '公司管理员', // 公司角色
                state: '有效', // 状态
            },{
                number: 1, // 序号
                account: 'admin', // 账号
                name: '某某某', // 姓名
                company: '深圳市市政工程有限公司', // 所属公司
                role: '公司管理员', // 公司角色
                state: '无效', // 状态
            }], // 表格数据
            page: 1, // 当前页码
            pageSize: 10, // 每页显示条数
            pageTotal: 0, // 总条数
            dialogShow: false, // 对话框显示状态

            // 对话框数据
            id: '', // 当前选中的账号id
            userName: '', // 姓名
            userPhone: '', // 联系电话
            userAccount: '', // 账号
            userPassword: '', // 密码
            userState: '', // 账户状态
            userType: 2, // 账户类型
            entry: '', // 登录权限
            ids: '', // 角色id字符串
            userStateOptions: [
                {
                    value: '1',
                    label: '启用'
                },
                {
                    value: '0',
                    label: '禁用'
                }
            ], // 账户状态选项
            entryOptions: [
                {
                    value: '0',
                    label: 'APP'
                },
                {
                    value: '1',
                    label: 'PC'
                },
                {
                    value: '2',
                    label: 'APP+PC'
                }
            ], // 登录项选项
        }
    },
    created() {
        this.querySystemUserList()
        this.querySystemPrivileges()
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

        // 验证账号是否存在
        selectSystemUser() {
            this.$axios.post(`/api/system/computer/selectSystemUser?userAccount=${this.userAccount}`).then(
                res => {
                    console.log(res.data.code)
                    if (res.data.code != 0) {
                        this.$message({
                            message: `${res.data.msg}`,
                            type: 'warning'
                        })
                    }
                }
            )
        },

        // 获取账号列表
        querySystemUserList () {
            this.$axios.post(`/api/system/computer/querySystemUser?userType=1&parameterId=1&page=${this.page}&pageSize=${this.pageSize}`).then(
                res => {
                    console.log(res.data)
                }
            )
        },

        // 获取所有权限
        querySystemPrivileges() {
            this.$axios.post(`/provider/systemPrivileges/pc/querySystemPrivileges`).then(
                res => {
                    console.log(res.data)
                }
            )
        },

        // 创建账号
        querySystemUser() {
            if (this.userName && this.userPhone && this.userAccount && this.userPassword && this.userState && this.entry) {
                this.$axios.post(`/api/system/computer/insertSystemUser?publicId=1&userName=${this.userName}&userPhone=${this.userPhone}&userAccount=${this.userAccount}&userPassword=${this.userPassword}&userState=${this.userState}&userType=${this.userType}&entry=${this.entry}&ids=${this.ids}`).then(
                    res => {
                        if (res.data.code == 0) {
                            this.$message({
                                message: '添加成功',
                                type: 'success'
                            })
                            this.dialogShow = false
                            this.pageNum = 1
                            this.querySystemUserList()
                        } else {
                            this.$message({
                                message: `${res.data.msg}`,
                                type: 'warning'
                            })
                        }
                    }
                )
            } else {
                this.$message({
                    message: '带 * 号的输入框不得为空',
                    type: 'warning'
                })
            }
        },
    }
}
</script>