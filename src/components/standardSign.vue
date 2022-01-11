<template>
    <div class="sign-page-box">
        <!-- 头部 -->
        <div class="top-header">
            <h3>标准签章模式</h3>
            <span>更换签章模式</span>
        </div>
        <!-- 内容部分 -->
        <div class="bot-cont-box">
            <div class="left-box">
                <div class="left-inner-header">
                    安全签演示平台实例合同
                </div>
                <div class="left-cont-box">
                    <!-- 侧边栏部分 -->
                    <div class="nav-list"  :style="{
                        width:`${navListWidth}px`
                    }">
                        <leftList :unfold="unfold" @setUnfold="setUnfold"></leftList>
                    </div>
                    <!-- 文章区域 -->
                    <div class="file-box" :style="{
                        width:`calc(100% - ${navListWidth}px)`
                    }">
                        <contractList></contractList>
                    </div>
                </div>
            </div>
            <div class="right-box">
                操作区域
            </div>
        </div>
    </div>
</template>
<script>
import leftList from "./leftList.vue"
import contractList from "./contractList.vue";
export default{
    components:{
        leftList,
        contractList
    },
    data(){
        return{
            navListWidth:200,//左边小图列表宽度,
            unfold:true,//控制侧边栏是否展示
        }
    },
    methods:{
        setUnfold(){
            this.unfold = !this.unfold;
            this.unfold?this.navListWidth=200:this.navListWidth=0
        }
    }
}
</script>、
<style lang="less" scoped>
.sign-page-box{
    height: calc(100vh - @headerHeight);
    overflow: hidden;
    width: 100%;
    padding: 15px;
    padding-bottom: 0;
    .top-header{
        width: 100%;
        height: 30px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 24px;
        background: #fff;
        margin-bottom: 15px;
        h3{
            font-size: 13px;
            padding-left: 14px;
            letter-spacing: 1px;
            position: relative;
            &::before{
                content: '';
                position: absolute;
                left: 0;
                width: 4px;
                height: 100%;
                border-radius: 4px;
                background: red;
            }
        }
    }
    .bot-cont-box{
        height: calc(100vh - 60px - @headerHeight);
        width: 100%;
        overflow: hidden;
        display: flex;
        justify-content: space-between;
        .left-box{
            background: #fff;
            display: flex;
            flex-direction: column;
            width:calc(100% - 315px);
            height: 100%;
            .left-inner-header{
                width: 100%;
                display: flex;
                height: 30px;
                font-size: 13px;
                align-items: center;
                position: relative;
                padding-left: 38px;
                &::after{
                    content: ' ';
                    position: absolute;
                    bottom: 0;
                    left: 0;
                    height: 1px;
                    width: 100%;
                    background: @u-border-color;
                }
            }
            .left-cont-box{
                height: calc(100% - 30px);
                box-sizing: border-box;
                display: flex;
                justify-content: space-between;
                .nav-list{
                    height: 100%;
                    border-right: 1px solid @u-border-color;
                    overflow-y: auto;
                    
                }
            }
        }
        .right-box{
            width: 300px;
            // height: calc(100% - 30px);
            background: #fff;
        }
    }
}
</style>