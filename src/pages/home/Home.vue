<template>
    <div>
        <home-header :city="city"/>
        <home-swiper :list="swiperList"/>
        <home-icons :icon="iconList"/>
        <home-recommend :list="recommendList"/>
        <home-weekend :list="weekendList"/>
    </div>
</template>

<script>
import HomeHeader from './components/Header'
import HomeSwiper from './components/Swiper'
import HomeIcons from './components/Icons'
import HomeRecommend from './components/Recommend'
import HomeWeekend from './components/Weekend'
import axios from 'axios'
import {mapState} from 'vuex';
export default {
    name: 'Home',
    components:{
        HomeHeader,
        HomeSwiper,
        HomeIcons,
        HomeRecommend,
        HomeWeekend
    },
    data(){
        return {
            lastCity:'',
            city:'',
            swiperList: [],
            iconList: [],
            recommendList: [],
            weekendList: []
        }
    },
    methods:{
        getHomeInfo(){
            axios.get('/api/index.json?city='+this.city)
            .then(this.gethomeInfoSucc)
        },
        gethomeInfoSucc(res){
            res = res.data;
            console.log(res)
            if(res.ret&&res.data){
                const data = res.data;
                this.city = data.city;
                this.swiperList = data.swiperList;
                this.iconList = data.iconList;
                this.recommendList = data.recommendList;
                this.weekendList = data.weekendList;
            }
        }
    },
    mounted(){
        this.lastCity = this.city;
        this.getHomeInfo();
    },
    activated() {
        if(this.lastCity!==this.city){
            this.lastCity = this.city;
            this.getHomeInfo();
        }
    },
    computed: {
        ...mapState(['city'])
    }
}
</script>

<style scoped>

</style>