<template>
    <div>
        <router-link v-show="showAbs" tag="div" to="/" class="header-abs">
            <div class="iconfont">&#xe624;</div>
        </router-link>
        <div :style="opactityStyle" v-show="!showAbs" class="header-fixed">
            景点详情
            <router-link to="/">
                <div class="iconfont header-left">&#xe624;</div>
            </router-link>
        </div>
    </div>
</template>

<script>
    export default {
        name: "",
        data() {
            return {
                showAbs: true,
                opactityStyle: {
                    opactity: 0
                }
            }
        },
        methods: {
            handleScroll() {
                const top = document.documentElement.scrollTop;
                if (top > 30) {
                    let opacity = top / 100 > 1 ? 1 : top / 100;
                    this.opactityStyle = {
                        opacity
                    }
                    this.showAbs = false;
                } else {
                    this.showAbs = true;
                }

            }
        },
        activated() {
            window.addEventListener('scroll', this.handleScroll);
        },
        deactivated() {
            window.removeEventListener('scroll', this.handleScroll);
        }
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    @import "~styles/varibles.styl";
    .header-abs
        position absolute
        left .2rem
        top .2rem
        width .8rem
        height .8rem
        border-radius .4rem
        text-align center
        line-height .8rem
        color #fff
        background rgba(0, 0, 0, 0.8)
        .iconfont
            font-size .4rem

    .header-fixed
        overflow hidden
        height $headerHeight
        line-height $headerHeight
        text-align center
        color #fff
        background $bgColor
        font-size .32rem
        position fixed
        top 0
        left 0
        right 0
        z-index 2

        .header-left
            width .64rem
            text-align center
            position absolute
            top 0
            left 0
            color #fff
</style>