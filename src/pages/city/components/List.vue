<template>
    <scroll class="list" ref="cityList" :probeType="3" @scroll="scroll" :listenScroll="true">
        <div>
            <div class="area">
                <div class="title border-topbottom">当前城市</div>
                <div class="button-list">
                    <div class="button-wrapper">
                        <div class="button">
                            广州
                        </div>
                    </div>
                </div>
            </div>
            <div class="area">
                <div class="title border-topbottom">热门城市</div>
                <div class="button-list">
                    <div class="button-wrapper" v-for="hotCitie in hotCities">
                        <div class="button">
                            {{hotCitie.name}}
                        </div>
                    </div>
                </div>
            </div>

            <div class="area">
                <div v-for="(citie,index) in cities" ref="cityLi">
                    <div class="title border-topbottom">{{citie.title}}</div>
                    <div class="item-list" v-for="item in citie.items">
                        <div class="item border-bottom">{{item.name}}</div>
                    </div>
                </div>
            </div>

        </div>
        <ul class="shortcut">
            <li v-for="(citie,index) in shortcutList" :class="{'current':currentIndex===index}"
                @click="toShortCut(index)">
                {{citie}}
            </li>
        </ul>
    </scroll>
</template>

<script>
    import Scroll from 'common/scroll/Scroll'
    import axios from 'axios'

    export default {
        name: "",
        data() {
            return {
                hotCities: [],
                cities: [],
                scrollY: -1,
                currentIndex: 0,
                diff: -1
            }
        },
        created() {
            this.initCity();
        },
        computed: {
            shortcutList() {
                return this.cities.map((group) => {
                    return group.title.substr(0, 1);
                });
            },
        },
        methods: {
            initCity() {
                axios.get('/api/city.json').then((res) => {
                    this.hotCities = res.data.data.hotCities;
                    this.cities = this.fromData(res.data.data.cities);
                })
            },
            toShortCut(index) {
                this.currentIndex = index;
                this.$refs.cityList.scrollToElement(this.$refs.cityLi[index], 500);
            },
            scroll(pos) {
                this.scrollY = pos.y;

            },
            fromData(data) {
                let map = {};
                let ret = [];//用于放是字母的数组
                for (let key in data) {
                    if (key.match(/[a-zA-Z]/)) {
                        if (!map[key]) {
                            map[key] = {
                                title: key,
                                items: data[key]
                            }
                        }
                        ret.push(map[key]);
                    }
                }
                // 对数组进行排序
                return ret.sort((a, b) => {
                    //将A-Z转换在成Unicode编码再进行对比排序
                    return a.title.charCodeAt(0) - b.title.charCodeAt(0);
                });
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
            }
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
            top 15%
            right 0
            li
                line-height .4rem
                background #ccc
                text-align center
            .current
                color #fff
                background #00bcd4

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

</style>