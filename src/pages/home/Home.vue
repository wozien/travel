<template>
    <div class="home-page">
        <home-header></home-header>
        <home-swiper :list="swiperList"></home-swiper>
        <home-icons :list="iconList"></home-icons>
        <home-recommend :list="recommendList"></home-recommend>
        <home-weekend :list="weekendList"></home-weekend>
    </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import { mapState } from 'vuex'
import axios from 'axios'

export default {
    name: 'Home',
    components: {
        HomeHeader,
        HomeSwiper,
        HomeIcons,
        HomeRecommend,
        HomeWeekend
    },
    data () {
        return {
            lastCity: '',
            swiperList: [],
            iconList: [],
            recommendList: [],
            weekendList: []
        }
    },
    computed: {
        ...mapState(['city'])
    },
    mounted () {
        this.getHomeInfo();
        this.lastCity = this.city;
    },
    activated () {
        // 判断当前城市是否更新，更新了再去请求数据
        if(this.lastCity !== this.city) {
            this.lastCity = this.city;
            this.getHomeInfo();
        }
    },
    methods: {
        getHomeInfo () {
            axios.get('/api/index.json?city=' + this.city)
                 .then(this.getHomeInfoSucc);
        },
        getHomeInfoSucc (res) {
            res = res.data;
            if(res.ret && res.data) {
                const data = res.data;
                this.swiperList = data.swiperList;
                this.iconList = data.iconList;
                this.recommendList = data.recommendList;
                this.weekendList = data.weekendList;
            }
        }
    }
}
</script>

<style lang="stylus" scoped>
.home-page
    background #f5f5f5
</style>

