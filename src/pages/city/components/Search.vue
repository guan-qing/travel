<template>
    <div class="search">
        <input class="search-input" type="text" placeholder="输入城市名或拼音">
    </div>
</template>

<script>
    export default {
        name: ""
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
</style>