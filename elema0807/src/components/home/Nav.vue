<template>
    <!-- 导航栏 -->
    <div>
        <transition name="fade">
        <div class="small-cover" v-show="isShow"></div>
        </transition>

        <div class="big-cover"  v-show="isShow" @click="hideNav()"></div>
        <div class="nav" ref='navs'>
            <!-- 综合排序 -->
            <div class="rank" @click="rankAction()">
                {{sortTitle}}▼
            </div>

            <div class="rankAll" v-show="rankAllData" ref="sortAll">
                <li v-for="(item,index) in rankArr" :key='index'
                @click="pitchAction(index)">{{rankArr[index]}}</li>
            </div>

            <!-- 距离最近 -->
            <div class="distance">
                距离最近
            </div>

            <!-- 品质联盟 -->
            <div class="quality">
                品质联盟
            </div>

            <!-- 筛选 -->
            <div class="filt" @click="filtAction()">
                筛选 ↓
            </div>

            <div class="filtAll" v-show="filtAllData">
                <div class="multiple">
                    <p class="multipletitle">商家服务（可多选）</p>
                    <div class="multiple-arr">
                        <li v-for="(item,index) in multipleArr" :key="index">
                            <img :src="multipleImgArr[index]" alt="">{{multipleArr[index]}}
                        </li>
                    </div>
                </div>

                <div class="radio">
                    <p class="radiotitle">优惠活动（单选）</p>
                    <div class="radio-arr">
                        <li v-for="(item,index) in radioArr" :key="index">
                            {{radioArr[index]}}
                        </li>
                    </div>
                </div>
                
                <div class="pay">
                    <p class="paytitle">人均消费</p>
                    <div class="pay-arr">
                        <li v-for="(item,index) in payArr" :key="index">
                            {{payArr[index]}}
                        </li>
                    </div>
                </div>

                <div class="paysure">
                    <div class="paysure-left">清空</div><div class="paysure-right">确定</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            isShow:false,
            sortTitle:'综合排序',
            rankAllData:false,
            filtAllData:false,
            rankArr:[
                '综合排序',
                '好评优先',
                '销量最高',
                '起送价最低',
                '配送最快',
                '配送费最低',
                '人均从低到高'
            ],
            multipleArr:[
                '蜂鸟专送',
                '品牌商家',
                '食安保',
                '新店',
                '开发票'
            ],
            multipleImgArr:[
                '//fuss10.elemecdn.com/b/9b/45d2f6ff0dbeef3a78ef0e4e90abapng.png?imageMogr/format/webp/thumbnail/!24x24r/gravity/Center/crop/24x24/',
                '//fuss10.elemecdn.com/6/7c/417ba499b9ef8240b8014a453bf30png.png?imageMogr/format/webp/thumbnail/!24x24r/gravity/Center/crop/24x24/',
                '//fuss10.elemecdn.com/2/cd/444d002a94325c5dff004fb3b9505png.png?imageMogr/format/webp/thumbnail/!24x24r/gravity/Center/crop/24x24/',
                '//fuss10.elemecdn.com/c/93/ded991df780906f7471128a226104png.png?imageMogr/format/webp/thumbnail/!24x24r/gravity/Center/crop/24x24/',
                '//fuss10.elemecdn.com/3/d4/5668ffc03151826f95b75249bea31png.png?imageMogr/format/webp/thumbnail/!24x24r/gravity/Center/crop/24x24/'
            ],
            radioArr:[
                '新用户优惠',
                '特价商品',
                '下单立减',
                '赠品优惠',
                '下单返红包',
                '进店领红包'
            ],
            payArr:[
                '￥20以下',
                '￥20-￥40',
                '￥40-￥60',
                '￥60-￥80',
                '￥80-￥100',
                '￥100以上'
            ]
        }
    },

    methods:{
        rankAction(){
            this.isShow = !this.isShow;
            this.$refs.navs.style.position = 'absolute';
            this.$refs.navs.style.top = 0;
            this.rankAllData = !this.rankAllData;
            this.filtAllData = false;
        },

        filtAction(){
            this.filtAllData = !this.filtAllData;
            this.rankAllData = false;
            this.isShow = !this.isShow;
            this.$refs.navs.style.position = 'absolute';
            this.$refs.navs.style.top = 0;
        },

        pitchAction(index){

            this.sortTitle = this.rankArr[index];
        
        },

        hideNav(){
            console.log(9191919)
            this.isShow = !this.isShow;
            this.$refs.navs.style.position = '';
            this.$refs.navs.style.top = '';
            this.rankAllData = false;
            this.filtAllData = false;
        }

    }
}
</script>

<style scoped>
    .big-cover{
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        background: transparent;
        z-index: 15;
    }
    .small-cover{
        z-index: 5;
        width: 100%;
        position: absolute;
        top: 50px;
        bottom: 0;
        left: 0;
        background: rgba(0,0,0,0.5);
    }
    @keyframes fadeIn {
        0%{opacity: 0}
        100%{opacity: 1}
    }
    @keyframes fadeOut {
        0%{opacity: 1}
        100%{opacity: 0}
    }
    .fade-enter-active{
        animation: fadeIn 200ms;
    }
    .fade-leave-active{
        animation: fadeOut 200ms;
    }

    .nav{
        background: #fff;
        width: 100%;
        height: 40px;
        color: #666;
        font-size: 14px;
        display: flex;
        text-align: center;
        line-height: 40px;
        justify-content: space-between;
        position: relative;
    }

    .rank{
        flex: 1;
    }

    .rankAll{
        height: 100%;
        width: 100%;
        position: absolute;
        left: 5px;
        top: 40px;
        line-height: 40px;
        background: #fff;
    }

    .rankAll li{
        box-sizing: border-box;
        padding-left: 14px;
        background: #fff;
        width: 100%;
        position: relative;
        left: -5px;
        z-index: 10;
        text-align: left;
        border-bottom: 1px dotted #eee;
    }
    

    .distance{
        flex: 1
    }

    .quality{
        flex: 1
    }

    .filt{
        flex: 1
    }

    .filtAll{
        box-sizing: border-box;
        position: absolute;
        top: 40px;
        /* left: 5px; */
        overflow: auto;
        height: 350px;
        z-index: 10;
        background: #fff;
    }

    .multiple-arr img{
        display: inline-block;
        width: 13px;
        height: 13px;
        position: relative;
        left: -3px;
        top: 1px;
    }
    .multipletitle,.radiotitle,.paytitle{
        box-sizing: border-box;
        color: #666;
        font-size: 12px;
        height: 15px;
        line-height: 15px;
        width: 100%;
        margin-bottom: 5px;
        float: left;
        display: flex;
        justify-content: flex-start;
    }

    .filtAll li{
        width: 33%;
        height: 35px;
        line-height: 35px;
        text-align: center;
        float: left;
        z-index: 10;
        background: #fff;
    }

    .paysure{
        width: 100%;
        height: 44px;
        display: flex
    }

    .paysure-left{
        flex: 1;
        background: #fff;
        color: #666;
        line-height: 44px;
        text-align:center;
    }

    .paysure-right{
        flex: 1;
        color: #fff;
        background: #00d762;
        line-height: 44px;
        text-align:center;
    }


















</style>
