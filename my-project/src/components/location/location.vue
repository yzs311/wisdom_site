<template>
    <div id="location">
        <!-- 侧导航栏 -->
        <div class="select">
            <ul>
                <!-- <li @click="isActive='/location/l_homePage'">
                    <router-link to="/location/l_homePage" :class="isActive=='/location/l_homePage'?'active':''">
                        <i class="homePage"></i>
                        首页
                    </router-link>
                </li> -->
                <li @click="isActive='/location/l_monitoring'">
                    <router-link to="/location/l_monitoring" :class="isActive=='/location/l_monitoring'?'active':''">
                        <i class="location"></i>
                        实时监控
                    </router-link>
                </li>
                <li @click="isActive='/location/l_search'">
                    <router-link to="/location/l_search" :class="isActive=='/location/l_search'?'active':''">
                        <i class="search"></i>
                        搜索查询
                    </router-link>
                </li>
                <li @click="isActive='/location/l_rail'">
                    <router-link to="/location/l_rail" :class="isActive=='/location/l_rail'?'active':''">
                        <i class="rail"></i>
                        电子围栏
                    </router-link>
                </li>
                <li @click="isActive='/location/l_history'">
                    <router-link to="/location/l_history" :class="isActive=='/location/l_history'?'active':''">
                        <i class="statisti"></i>
                        历史轨迹
                    </router-link>
                </li>
                <!-- <li @click="isActive='/location/l_set'">
                    <router-link to="/location/l_set" :class="isActive=='/location/l_set'?'active':''">
                        <i class="system"></i>
                        系统设置
                    </router-link>
                </li> -->
            </ul>
        </div>
        <!-- 内容区域 -->
        <router-view class="router-box"></router-view>
    </div>
</template>

<style lang="less" scoped>
    #location {
        padding:  .5rem .4rem 0 .4rem;
        display: flex;
        .select {
            width: 3rem;
            height: 9.41rem;
            background-image: url('../../../static/images/m_left-border.png');
            background-size: contain;
            background-color: #020521;
            padding: .02rem;
            margin-right: .4rem;
            ul {
                li {
                    height: .57rem;
                    background-image: url('../../../static/images/m_select-border.png');
                    background-position: bottom center;
                    background-repeat: no-repeat;
                    background-size: 2.73rem .01rem;
                    a {
                        display: block;
                        width: 2.94rem;
                        height: .56rem;
                        color: #3979fe;
                        position: relative;
                        line-height: .56rem;
                        padding-left: .42rem;
                        i {
                            width: .17rem;
                            height: .17rem;
                            position: absolute;
                            background-size: contain;
                            left: .17rem;
                            top: 50%;
                            transform: translateY(-50%);
                        }
                        .homePage {
                            background-image: url('../../../static/images/location-homePage.png');
                        }
                        .location {
                            background-image: url('../../../static/images/location-location.png');
                        }
                        .rail {
                            background-image: url('../../../static/images/location-rail.png');
                        }
                        .statisti {
                            background-image: url('../../../static/images/location-statisti.png');
                        }
                        .system {
                            background-image: url('../../../static/images/location-system.png');
                        }
                        .search {
                            background-image: url('../../../static/images/location-search.png');
                        }
                    }
                    .active {
                        background-image: url('../../../static/images/location-active.png');
                        background-size: contain;
                    }
                }
            }
        }
        .router-box {
            flex: 1;
        }  
    }
</style>


<script>
export default {
    data() {
        return {
            isActive: '/location/l_monitoring',
        }
    },
    methods: {
        getRouter() {
            if (this.$route.path != '/location') {
                this.isActive = this.$route.path
            }
        }
    },
    created() {
        this.getRouter()
    },
    updated() {
        this.getRouter()
    },
}
</script>
