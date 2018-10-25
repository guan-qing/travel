<template>
    <div class="city">
        <city-header></city-header>
        <city-search></city-search>
        <city-list :hotCities="hotCities" :cities="cities" :tests="tests"></city-list>
    </div>
</template>

<script>
    import axios from 'axios'
    import CityHeader from './components/Header'
    import CitySearch from './components/Search'
    import CityList from './components/List'

    export default {
        name: "",
        components: {
            CityHeader,
            CitySearch,
            CityList
        },
        data() {
            return {
                hotCities: [],
                cities: [],
                tests: {}
            }
        },
        created() {
            this.initCity();
        },
        methods: {
            initCity() {
                axios.get('/api/city.json').then((res) => {
                    this.hotCities = res.data.data.hotCities;
                    this.cities = this.fromData(res.data.data.cities);
                    this.tests = res.data.data.cities;
                })
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
        }
    }
</script>

<style scoped lang="stylus" type="text/stylus">

</style>