<template>
    <div>
        <div class="search">
            <input class="search-input" type="text" placeholder="输入城市名或拼音" 
                   v-model="keyword">
        </div>
        <div class="search-content" ref="search" v-show="keyword">
            <ul>
                <li class="search-item border-bottom"
                    v-for="item of list"
                    :key="item.id"
                    @click="handleCityClick(item.name)">{{ item.name }}</li>
                <li class="search-item border-bottom" v-show="hasNoData">没有找到匹配数据</li>
            </ul>
        </div>
    </div>
    
</template>

<script>
import Bscroll from 'better-scroll'
import { mapMutations } from 'vuex'

export default {
    name: 'CitySearch',
    props: {
        cities: Object
    },
    data () {
        return {
            keyword: '',
            timer: null,
            list: []
        }
    },
    mounted () {
        this.scroll = new Bscroll(this.$refs.search);
    },
    computed : {
        hasNoData () {
            return !this.list.length;
        }
    },
    watch: {
        keyword () {
            if(this.timer) {
                clearTimeout(this.timer);
            }
            this.timer = setTimeout(() => {
                if(!this.keyword) {
                    this.list = [];
                    return;
                }
                const result = [];
                for(let i in this.cities) {
                    this.cities[i].forEach((value) => {
                        if(value.spell.indexOf(this.keyword) > -1 ||
                            value.name.indexOf(this.keyword) > -1) {
                                result.push(value)
                            }
                    })
                }
                this.list = result;
            }, 100);
        }
    },
    methods: {
        handleCityClick (city) {
            this.changeCity(city);
            this.$router.push('/');
        },
        // 将vuex中mutations里面的方法映射成自己的方法
        ...mapMutations(['changeCity'])
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'

.search
    height .72rem
    background $bgColor
    padding 0 .1rem
    .search-input
        box-sizing border-box
        width 100%
        height .62rem
        line-height .62rem
        text-align center
        color #666666
        border-radius .06rem
        padding 0 .1rem
.search-content
    z-index 1
    overflow hidden
    position absolute 
    top 1.58rem
    left 0 
    right 0
    bottom 0
    background #eee
    .search-item
        line-height .62rem
        padding-left .2rem
        background #ffffff
        color #666
</style>


