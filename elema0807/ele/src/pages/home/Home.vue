<template>
<page ref="foods" :onScroll="handlePageScroll">
    <div>
     
        <div class="warp">
            <!--首页头部 -->
            <div class="head">
                <div class="headTop">
                    <span></span><span>深圳西部硅谷</span><span>↓</span>
                </div>
                <div class="headInp">
                    <input type="text" placeholder="搜索饿了么商家、商品名称">
                </div>   
            </div>
            <!-- 首页轮播 -->
            <Banner></Banner>
            
            <!-- 首页抢购部分  -->
                <Activity></Activity>
            <!-- 餐馆列表  -->
                <food-list v-for="(item,index) in restaurantsData" :key="index" :resdata="item"  ></food-list>
        </div>
        
            
    </div>
</page>

</template>

<script>
import {getHomeAddressData,getHomebannerGoodsData,getHomeRestaurantsData} from './../../services/homedata.js'
import Banner from '@/components/home/Banner.vue'

import FoodList  from  './../../components/foodlist/FoodList.vue' 
import Activity from '@/components/home/Activity.vue'
import Page from '@/components/page/Page.vue'
export default {
    components:{
        Banner,
        FoodList,
        Activity,
        Page
},
    data(){
        return{
           restaurantsobj:{
                latitude:22.63336,        //纬度
                longitude:113.814549,      //经度 
                offset:0,
                limit:8,
                
           },
            restaurantsData:[],
            cancelRequestRestaurant:true,
        }
    },
    methods:{
        // 判断返回距离底部的值
       handlePageScroll(y){
            if(y < 50 && this.cancelRequestRestaurant){
                this.restaurantsobj.offset+=8;
                this.requestRestaurantsdata()

                console.log(this.cancelRequestRestaurant)
               
            }
        },
        requestRestaurantsdata(){
            this.cancelRequestRestaurant=false;
            getHomeRestaurantsData(this.restaurantsobj).then(result=>{
            this.restaurantsData=[...this.restaurantsData, ...result];
            this.$nextTick(()=>{
                    //更新dom
                    this.$refs.foods.refreshDOM();
                    //计算
                   this.cancelRequestRestaurant=true;
                })



             })
        }
       
    },
    created(){
        this.requestRestaurantsdata();

    },
    mounted(){
                 
            this.$center.$on('refreshDom',()=>{
                 console.log('更新dom')
            this.$nextTick(()=>{
                this.$refs.foods.refreshDOM();
            })
        })
       }
       
  
}
    
</script>

<style scoped>
    .head{
        
        height: 90px;
        background: #0085ff;
        padding: 10px 10px 0 10px;
    }

    .headTop{
        color: #fff;
        margin-bottom: 10px;
    }

    .headInp input{
        width: 100%;
        height: 40px;
        border: none;
        text-align: center
    }
    
</style>
