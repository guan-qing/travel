<template>
    <div>
        <detail-banner :gallaryImgs="gallaryImgs" :sightName="sightName" :bannerImg="bannerImg"></detail-banner>
        <detail-header></detail-header>
        <detail-list :list="list"></detail-list>
    </div>
</template>

<script>
    import DetailBanner from './components/Banner';
    import DetailHeader from './components/Header';
    import DetailList from './components/List';
    import axios from 'axios';

    export default {
        name: "Detail",
        data() {
            return {
                list: [],
                gallaryImgs: [],
                sightName: '',
                bannerImg: '',
            }
        },
        created() {
            this.getDetailInfo();
        },
        methods: {
            getDetailInfo() {
                axios.get('/api/detail.json', {
                    params: {
                        id: this.$route.params.id
                    }
                }).then((res) => {
                    this.list = res.data.data.categoryList;
                    this.sightName = res.data.data.sightName;
                    this.bannerImg = res.data.data.bannerImg;
                    this.gallaryImgs = res.data.data.gallaryImgs;
                });
            }
        },
        components: {
            DetailBanner,
            DetailHeader,
            DetailList
        },

    }
</script>

<style scoped lang="stylus" type="text/stylus">
    .content
        height 50rem
</style>