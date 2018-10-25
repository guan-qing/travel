<template>
    <div class="city">
        <city-header></city-header>
        <city-search></city-search>
        <city-list></city-list>
    </div>
</template>

<script>
    import CityHeader from './components/Header'
    import CitySearch from './components/Search'
    import CityList from './components/List'

    export default {
        name: "",
        components: {
            CityHeader,
            CitySearch,
            CityList
        }
    }
</script>

<style scoped lang="stylus" type="text/stylus">

</style>