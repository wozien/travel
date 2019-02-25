<template>
    <div class="gallary-container" @click="closeGallary">
        <div class="wrapper">
            <swiper :options="swiperOption">
                <swiper-slide v-for="(item, index) in imgs" :key="index">
                    <img :src="item" class="gallary-img"/>
                </swiper-slide>
                <div class="swiper-pagination" slot="pagination"></div> 
            </swiper>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CommonGallary',
    props: {
        imgs: Array
    },
    data () {
        return {
            swiperOption: {
                pagination: '.swiper-pagination',
                paginationType: 'fraction',   // 分页样式
                observeParents: true,      // 当父级dom变化时刷新组件，重新计算宽高
                observer: true
            }
        }
    },
    methods: {
        closeGallary () {
            this.$emit('close');
        }
    }
}
</script>

<style lang="stylus" scoped>
.gallary-container >>> .swiper-container
    overflow inherit
.gallary-container
    display flex
    flex-direction column
    justify-content center
    position fixed
    top 0
    right 0
    bottom 0
    left 0
    background #000
    z-index 99
    .wrapper
        height 0
        padding-bottom 100%
        .gallary-img
            width 100%
        .swiper-pagination
            color #fff
            bottom -1rem
</style>


