<template>
    <div>
        <div class="title">周末游玩</div>
        <ul class="item-container">
            <li class="item border-bottom"
                v-for="item of list" :key="item.id">
                <div class="item-img-wrapper">
                    <img :src="item.imgUrl" class="item-img">
                </div>
                <div class="item-info">
                    <p class="item-title">{{ item.title }}</p>
                    <p class="item-desc">{{ item.desc }}</p>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'HomeWeekend',
    props: {
        list: Array
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/mixins.styl'

.title
    line-height .8rem
    background #eee
    text-indent .2rem

.item-container
    background #f5f5f5

.item
    margin-bottom .1rem
    background #fff

.item-img-wrapper
    overflow hidden
    height 0
    padding-bottom 37.4375%
    .item-img
        width 100%

.item-info
    padding .2rem
    .item-title
        line-height .48rem
        font-size .28rem
        color #212121
        ellipsis()
    .item-desc
        line-height .42rem
        font-size .24rem
        color #616161
        ellipsis()

</style>


