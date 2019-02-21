<template>
    <div class="header">
        <div class="header-left">
            <div class="iconfont back-icon">&#xe624;</div>
        </div>
        <div class="header-input">
            <span class="iconfont">&#xe6ac;</span>
            输入城市/景点/游玩主题
        </div>
       <router-link to="/city">
           <div class="header-right">
                {{ this.city }}
                <span class="iconfont arrow-icon">&#xe64a;</span>
            </div>
       </router-link>
    </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
    name: 'Home',
    computed: {
        // 将vuex中的state的属性映射成自己的属性
        ...mapState(['city'])
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header
    display flex
    line-height $headerHight
    background #00bcd4
    color #fff
    .header-left
        width .64rem
        float left
        .back-icon
            text-align center
            font-size .4rem
    .header-input
        flex 1
        background #ffffff
        border-radius .1rem
        height .64rem
        line-height .64rem
        margin-top .12rem
        margin-left .2rem
        padding-left .2rem
        color #ccc
    .header-right
        min-width 1.04rem
        padding 0 .1rem
        float right
        text-align center
        color #fff
        .arrow-icon
            font-size .24rem
            margin-left -.04rem
</style>