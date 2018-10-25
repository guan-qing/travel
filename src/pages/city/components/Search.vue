<template>
    <div>

        <div class="search">
            <input v-model="keyword" class="search-input" type="text" placeholder="输入城市名或拼音">
        </div>
        <Scroll class="search-content" v-show="keyword">
            <ul>
                <li class="search-item" v-for="item in list">{{item.name}}</li>
            </ul>
        </Scroll>
    </div>
</template>

<script>
    import Scroll from 'common/scroll/Scroll'

    export default {
        name: "",
        props: {
            cities: Object
        },
        data() {
            return {
                keyword: '',
                list: [],
                timer: null
            }
        },
        watch: {
            keyword() {
                if (this.timer) {
                    clearTimeout(this.timer)
                }
                this.timer = setTimeout(() => {
                    const resilt = [];
                    for (let i in this.cities) {
                        this.cities[i].forEach((value) => {
                            if (value.spell.indexOf(this.keyword) > -1 || value.name.indexOf(this.keyword) > -1) {
                                resilt.push(value);
                            }
                        })
                    }
                    this.list = resilt;
                }, 100)
            }
        },
        components: {Scroll}
    }
</script>

<style scoped lang="stylus" type="text/stylus">
    @import "~styles/varibles.styl";
    .search
        height .72rem
        background $bgColor
        padding .1rem
        .search-input
            box-sizing border-box
            width 100%
            height .62rem
            line-height .62rem
            text-align center
            border-radius .06rem
            color #666
            padding 0 .1rem

    .search-content
        position absolute
        top 1.8rem
        overflow hidden
        right 0
        left 0
        bottom 0
        z-index: 1
        background #eee
        .search-item
            line-height .62rem
            padding-left .2rem
            color #666
            background #fff
            margin .1rem 0

</style>