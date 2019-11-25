<template>
    <div>
        <detail-banner/>
        <detail-header/>
        <div class="content">
            <detail-list :list='list'/>
        </div>
    </div>
</template>

<script>
import DetailBanner from './components/Banner';
import DetailHeader from './components/Header';
import DetailList from './components/List';

export default {
    name: 'Detail',
    components:{
        DetailBanner,
        DetailHeader,
        DetailList
    },
    data() {
        return {
            list: [{
                title: '成人票',
                children: [{
                    title: '成人三馆联票',
                    children: [{
                        title: '成人三馆联票1'
                    },{
                        title: '成人五馆联票2'
                    }]
                },{
                    title: '成人五馆联票'
                }]
            },{
                title: '儿童票'
            },{
                title: '老人票'
            },{
                title: '学生票'
            }]
        }
    }
}
</script>

<style lang="stylus" scope>
    
</style>