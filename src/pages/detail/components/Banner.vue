<template>
    <div>
        <div class="banner" @click="handleBannerClick">
            <img :src="bannerImg" class="banner-img">
            <div class="banner-info">
                <div class="banner-title">大连圣亚海洋世界(AAAA景区)</div>
                <div class="banner-number">
                    <span class="iconfont arrow-icon banner-icon">&#xe692;</span>
                    {{this.gallaryImgs.length}}
                </div>
            </div>
        </div>
        <common-gallary :imgs='gallaryImgs' v-show="showGallary" @close="handleGallaryColose"/>
    </div>
</template>

<script>
import CommonGallary from 'common/gallary/Gallary';
export default {
    name: 'DetailBanner',
    props:{
        sightName: String,
        bannerImg: String,
        gallaryImgs: Array
    },
    components:{
        CommonGallary
    },
    data() {
        return {
            showGallary: false
        }
    },
    methods:{
        handleBannerClick(){
            this.showGallary = true;
        },
        handleGallaryColose(){
            this.showGallary = false;
        }
    }
}
</script>

<style lang="stylus" scope>
    .banner
        position relative
        overflow hidden
        height 0
        padding-bottom 55%
        .banner-img
            width 100%
        .banner-info
            display flex
            position absolute
            left 0
            right 0
            bottom 0
            line-height .6rem
            color #fff
            background-image linear-gradient(top, rgba(0,0,0,0), rgba(0,0,0,0.8))
            .banner-title
                font-size .32rem
                flex 1
                padding 0 .2rem
            .banner-number
                margin-top .14rem 
                line-height .4rem
                padding 0 .4rem
                height .32rem
                border-radius .2rem
                font-size .24rem
                background rgba(0, 0, 0, .8)
                .banner-icon
                    font-size .24rem
</style>