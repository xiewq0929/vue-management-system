<template>
    <div class="header-container">
        <div class="l-content">
            <el-button style="margin-right:20px" @click="hanleMenu" icon="el-icon-menu" size="mini"></el-button>
            <el-breadcrumb separator="/">
                <el-breadcrumb-item v-for="item in tabsList" :key="item.path" :to="{ path: item.path}">{{item.label}}</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="r-content">
            <el-dropdown @command="handleCommand">
                <span class="el-dropdown-link">
                    <img class="user" src="../assets/images/2-3.jpg" alt="">
                </span>
                <el-dropdown-menu slot="dropdown">
                    <el-dropdown-item command="center">个人中心</el-dropdown-item>
                    <el-dropdown-item command="logout">退出</el-dropdown-item>
                </el-dropdown-menu>
            </el-dropdown>
        </div>
    </div>
</template>

<script>
    import {mapState} from 'vuex'
    export default {
        name:'CommonHeader',
        methods:{
            hanleMenu(){
                this.$store.commit('tab/collapseMenu')
            },
            handleCommand(command){
                if (command==="logout") {
                    //清除token信息
                    localStorage.removeItem('token')
                    localStorage.removeItem('menu')
                    //跳转到登录页
                    this.$router.push({
                        name:'login'
                    })
                }else{
                    this.$router.push({
                        name:'mall'
                    })
                }
            }
        },
        computed:{
            ...mapState('tab',['tabsList'])
        },
    }
</script>

<style lang='less' scoped>
    .header-container{
        height: 60px;
        padding: 0 20px;
        background-color: #333;
        display: flex;
        justify-content: space-between;
        align-items: center;
        .text{
            color: #fff;
            font-size: 14px;
            margin-left: 14px;
        }
        .r-content{
            .user{
                width: 40px;
                height: 40px;
                border-radius: 50%;
            }
        }
        .l-content{
            display: flex;
            align-items: center;
            /deep/.el-breadcrumb__item {
                .el-breadcrumb__inner{
                    font-weight: normal;
                    &.is-link{
                        color: #666;
                    }
                }
            }
            /deep/.el-breadcrumb__item:last-child{
                .is-link{
                    color: white;
                }
            }
        }
    }
</style>