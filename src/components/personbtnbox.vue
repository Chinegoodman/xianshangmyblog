<template>
    <div class="personbtnbox" @mouseover="mouseover()" @mouseout="mouseout()">
        <p v-if="!isloginstatus&&!ismouseover">游客</p>
        <p v-else-if="isloginstatus&&!ismouseover">{{nickname}}</p>

        <div class="btn" :class="{active:!isloginstatus && this.ismouseover}" @click="login">登录</div>
        <div class="btn" :class="{active:isloginstatus && this.ismouseover}" @click="logout">退登</div>
    </div>
</template>

<script>
    import eventbus from './../eventbus'
    export default {
        name: "personbtnbox",
        data(){
            return{
                nickname:'小庞',
                isloginstatus:true,
                ismouseover:false,
            }
        },
        methods:{
            mouseover(){
                this.ismouseover = true;
            },
            mouseout(){
                this.ismouseover = false;
            },
            login(){
                eventbus.$emit('mengbanstatus',true)
                eventbus.$emit('loginregistboxstatus',true)
            },
            logout(){

            }
        }
    }
</script>

<style scoped lang="less">
    @import "./../../public/common";
    @btnwidthheight:40px;
    .personbtnbox{
        background: @hoverbgcolorr;

        position: fixed;
        right: 5px;
        top: 5px;
        width: @btnwidthheight;
        height: @btnwidthheight;
        border-radius: 50%;
        overflow: hidden;
        p{
            text-align: center;
            line-height: 40px;
            font-size: @fontsizesmall;
            color: #fff;
        }
        div.btn{
            height: 100%;
            width: 100%;
            line-height: @btnwidthheight;
            color: @linkcoloractive;
            position: absolute;
            left: 100%;
            top: 0;
            transition: left 0.3s ease;
            &.active{
                left: 0;
            }
        }
        cursor: pointer;
    }
</style>