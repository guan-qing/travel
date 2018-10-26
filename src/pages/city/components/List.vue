<template>
    <scroll class="list" ref="cityList" :probeType="3" @scroll="scroll" :listenScroll="true">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">
                            {{city}}
                        </div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <div @click="handleCityClick(hotCitie.name)" class="button-wrapper" v-for="hotCitie in hotCities">
                        <div class="button">
                            {{hotCitie.name}}
                        </div>
                    </div>
                </div>
            </div>

            <div class="area">
                <div v-for="(citie,index) in cities" ref="cityLi">
                    <div class="title border-topbottom">{{citie.title}}</div>
                    <div class="item-list" @click="handleCityClick(item.name)" v-for="item in citie.items">
                        <div class="item border-bottom">{{item.name}}</div>
                    </div>
                </div>
            </div>
        </div>
        <ul class="shortcut" @touchstart.stop.prevent="onShortcutTouchStart"
            @touchmove.stop.prevent="onShortcutTouchMove">
            <li v-for="(citie,index) in shortcutList" :class="{'current':currentIndex===index}"
                @click="toShortCut(index)" :data-index="index">
                {{citie}}
            </li>
        </ul>
        <transition name="fade">
            <div class="toTop" v-show="showToTop" @click="toTop">
                <div>顶部</div>
            </div>
        </transition>
    </scroll>
</template>

<script>
    import Scroll from 'common/scroll/Scroll'
    import {mapState, mapMutations} from 'vuex';

    const ANCHOR_HEIGHT = 20
    export default {
        name: "",
        props: {
            hotCities: {
                type: Array
            },
            cities: {
                type: Array
            },
            tests: Object
        },
        data() {
            return {
                scrollY: -1,
                currentIndex: 0,
                diff: -1,
                timer: null,
                showToTop: false
            }
        },
        created() {
            this.touch = [];
        },
        computed: {
            shortcutList() {
                return this.cities.map((group) => {
                    return group.title.substr(0, 1);
                });
            },
            ...mapState(['city'])
        },
        methods: {
            toShortCut(index) {
                this.currentIndex = index;
                this._scrollTo(index);
            },
            scroll(pos) {
                this.scrollY = pos.y;
            },
            handleCityClick(name) {
                this.changeCity(name);
                //this.$store.commit('changeCity', name);
                this.$router.back();
            },
            onShortcutTouchStart(e) {
                let anchorIndex = this.getData(e.target, 'index');
                let firstTouch = e.touches[0];
                this.touch.y1 = firstTouch.pageY;
                this.touch.anchorIndex = anchorIndex;
                this._scrollTo(anchorIndex);
            },
            onShortcutTouchMove(e) {
                //this.timer用于性能优化
                if (this.timer) {
                    clearTimeout(this.timer);
                }
                this.timer = setTimeout(() => {
                    let firstTouch = e.touches[0];
                    this.touch.y2 = firstTouch.pageY;
                    let delta = (this.touch.y2 - this.touch.y1) / ANCHOR_HEIGHT | 0;
                    let anchorIndex = parseInt(this.touch.anchorIndex) + delta;
                    this._scrollTo(anchorIndex);
                }, 16)
            },
            toTop() {
                this.currentIndex = 0;
                this.showToTop = false;
                this.$refs.cityList.scrollTo(0, 0);
            },
            getData(el, name, val) {
                const prefix = "data-";
                name = prefix + name;
                if (val) {
                    return el.setAttribute(name, val);
                } else {
                    return el.getAttribute(name);
                }
            },
            _scrollTo(index) {
                if (!index && index !== 0) return;
                if (index < 0) {
                    index = 0;
                } else if (index > this.listHeight - 2) {
                    index = this.listHeight - 2;
                }
                this.scrollY = -this.listHeight[index];
                this.$refs.cityList.scrollToElement(this.$refs.cityLi[index], 100);
            },
            _calculateHeight() {
                this.listHeight = [];
                const list = this.$refs.cityLi;
                let height = 0;
                this.listHeight.push(height);
                for (let i = 0; i < list.length; i++) {
                    let item = list[i];
                    if (i == 0) {
                        height += item.clientHeight + 170;
                    } else {
                        height += item.clientHeight
                    }
                    this.listHeight.push(height);
                }
            },
            ...mapMutations(['changeCity'])
        },
        watch: {
            cities() {
                setTimeout(() => {
                    this._calculateHeight();
                }, 20)
            },
            scrollY(newY) {
                const listHeight = this.listHeight;
                // 当滚动到顶部,newY>0
                if (newY > 0) {
                    this.currentIndex = 0;
                    return;
                }
                //如果滚动到离顶部有500的距离则显示回到顶部按钮
                if (newY < -500 && !this.showToTop) {
                    this.showToTop = true;
                } else if (newY > -500 && this.showToTop) {
                    this.showToTop = false;
                }

                // 当在中间部分滚动
                for (let i = 0; i < listHeight.length - 1; i++) {
                    let height1 = listHeight[i];
                    let height2 = listHeight[i + 1];
                    if (-newY >= height1 && -newY < height2) {
                        this.currentIndex = i;
                        this.diff = height2 + newY;
                        return;
                    }
                }
                // 当滚动到低部,且-newY大于最后一个元素的上限
                this.currentIndex = listHeight.length - 2;
                console.log(this.currentIndex);
            },
            // diff(newVal) {
            //     let fixedTop = (newVal > 0 && newVal < TITLE_HEIGHT) ? newVal - TITLE_HEIGHT : 0;
            //     if (this.fixedTop == fixedTop) return;
            //     this.fixedTop = fixedTop;
            //     this.$refs.fixed.style.transform = `translate3d(0,${fixedTop}px,0)`;
            // }
        },
        components: {Scroll}
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    .border-topbottom
        &:before
            border-color #ccc
        &:after
            border-color #ccc

    .border-bottom
        &:before
            border-color #ccc

        &:after
            border-color #ccc

    .list
        overflow hidden
        position absolute
        top 1.8rem
        left 0
        right 0
        bottom 0
        .shortcut
            position absolute
            top 10%
            right 0
            li
                line-height .4rem
                text-align center
                color #00bcd4
            .current
                color #fff
                background #00bcd4
        .toTop
            position absolute
            right .5rem
            bottom .5rem
            width .8rem
            height .8rem
            line-height .8rem
            text-align center
            background #00BCD4
            border-radius 50%
            color #fff;

    .title
        line-height .5rem
        background #eee
        padding-left .2rem
        color #666
        font-size .26rem

    .button-list
        padding .1rem .6rem .1rem .1rem
        overflow hidden
        .button-wrapper
            float left
            width 33.33%
            .button
                text-align center
                margin .1rem
                padding .1rem 0
                border .02rem solid #ccc
                border-radius .06rem

    .item-list
        .item
            padding-left .2rem
            line-height .76rem

    .fade-enter-active, .fade-leave-active
        transition: all 0.5s
        opacity: 1
        transform: translate3d(0, 0, 0)

    .fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */
        opacity: 0;
        transform: translate3d(0, 100%, 0)


</style>