<template>
    <div>
        <router-link tag="div" to="/" class="header-abs" v-show="showAbs">
            <div class="iconfont header-abs-back">&#xe624;</div>
        </router-link>
        <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
            景点详情
            <router-link to="/">
                <div class="iconfont header-fixed-back">&#xe624;</div>
            </router-link>
        </div>
    </div>
</template>

<script>
export default {
    name: 'DetailHeader',
    data () {
        return {
            showAbs: true,
            opacityStyle: {
                opacity: 0
            }
        }
    },
    created () {
        window.addEventListener('scroll', this.handleScroll);
    },
    beforeDestroy () {
        window.removeEventListener('scroll', this.handleScroll);
    },
    methods: {
        handleScroll () {
            let top = document.documentElement.scrollTop;
            if(top > 60) {
                let opacity = top / 140;
                opacity = opacity > 1 ? 1 : opacity;
                this.$set(this.opacityStyle, 'opacity', opacity);
                this.showAbs = false;
            }else {
                this.showAbs = true;
            }
        }
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'

.header-abs
    position absolute
    left .2rem
    top .2rem
    width .8rem
    height .8rem
    line-height .8rem
    text-align center
    background rgba(0,0,0,.8)
    border-radius .4rem
    .header-abs-back
        color #fff
        font-size .4rem

.header-fixed
    position fixed
    top 0
    left 0
    right 0
    height $headerHight
    line-height $headerHight
    background $bgColor
    color #fff
    text-align center
    z-index 1
    .header-fixed-back
        position absolute
        top 0
        left 0
        width .64rem
        text-align center
        font-size .4rem
        color #fff

</style>

