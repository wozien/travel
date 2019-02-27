<template>
    <ul class="list">
        <li class="item" v-for="item of letters" :key="item" :ref="item"
            @click="handleClick"
            @touchstart.prevent="handleTouchStart"
            @touchmove="handleTouchMove"
            @touchend="handleTouchEnd">{{ item }}</li>
    </ul>
</template>

<script>
export default {
    name: 'CityAlphabet',
    props: {
        cities: Object
    },
    data () {
        return {
            touchStatus: false,
            startY: 0,
            timer: null
        }
    },
    computed: {
        letters () {
            return Object.keys(this.cities);
        }
    },
    updated () {
        // 当cities发生变化时触发
        this.startY = this.$refs['A'][0].offsetTop;
    },
    methods: {
        handleClick (e) {
            this.$emit('change', e.target.innerHTML);
        },
        handleTouchStart () {
            this.touchStatus = true;
        },
        // 触屏拖动事件
        handleTouchMove (e) {
            if(this.touchStatus) {
                // 进行防抖处理
                if(this.timer) {
                    clearTimeout(this.timer);
                }
                this.timer = setTimeout(() => {
                    let touchY = e.touches[0].clientY - 79;
                    let index = Math.floor((touchY - this.startY) / 20);
                    if(index >= 0 && index < this.letters.length) {
                        this.$emit('change', this.letters[index]);
                    }
                }, 16);
            }
        },
        handleTouchEnd () {
            this.touchStatus = false;
        }
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'

.list
    display flex
    flex-direction column
    justify-content center
    position absolute
    top 1.58rem
    right 0
    bottom 0
    width .4rem
    .item
        line-height .4rem
        text-align center
        color $bgColor
</style>


