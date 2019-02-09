<template>
    <div class="wrapper">
        <swiper :options="swiperOption">
            <swiper-slide v-for="item of list" :key="item.id">
                <img :src="item.imgUrl" class="swiper-img"/>
            </swiper-slide>
            <div class="swiper-pagination"  slot="pagination"></div> 
        </swiper>
    </div> 
</template>

<script>
export default {
    name: 'HomeSwiper',
    data () {
        return {
            swiperOption: {
                pagination: '.swiper-pagination',
                loop: true
            },
            list: [
                {
                    id: '001',
                    imgUrl: 'http://mp-piao-admincp.qunarzz.com/mp_piao_admin_mp_piao_admin/admin/20191/e9b6ede83785c7673eb1bcda5a78f123.jpg_750x200_0e6d0de9.jpg'
                },
                {
                    id: '002',
                    imgUrl: 'http://mp-piao-admincp.qunarzz.com/mp_piao_admin_mp_piao_admin/admin/20191/f4c1844c0a06ae46a11bc3c0f17c0b47.jpg_750x200_93c515e4.jpg'
                }
            ]
        }
    }
}
</script>

<style lang="stylus" scoped>
.wrapper >>> .swiper-pagination-bullet-active
    background: #fff
.wrapper  
    overflow hidden  
    width 100%
    height 0
    padding-bottom 26.67%
    background #eee
    .swiper-img
        width 100%
</style>

