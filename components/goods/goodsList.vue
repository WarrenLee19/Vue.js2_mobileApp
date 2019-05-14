<template>

<div>
    <!--调用方法getParams1，把里面的值传送到data中-->
<button v-on:click="getParams1" style="margin-left:300px;font-size: 17px;">录入客户住宿时间</button>
        <ul class="mui-table-view mui-grid-view">
            <li class="mui-table-view-cell mui-media mui-col-xs-6" v-for="item in productList">
                <a>
                    <img class="mui-media-object" v-bind:src="item.src">
                    <div class="desc">
                        <div class="sell">
                            <span>{{item.pro_price}}</span>
                            <strong>{{item.pro_name}}</strong>
                        </div>
                        <div class="detail">
                            <div class="hot">
                                {{item.pro_minutes}}分钟前有人下单
                            </div>

                            <div class="count" v-if="item.count1>10">
                            剩{{item.count1}}间

                            </div>
                            <div class="count" v-else="item.count1<10">
                                仅仅剩下{{item.count1}}间
                            </div>
                        </div>
                        <div style="text-align: right;"><button  @click="addCart(item.pro_name,item.pro_price,item.pro_btime,item.pro_etime,item.pro_num,item.src)">立即购买</button></div>
                    </div>
                </a>
            </li>

        </ul>
    </div>
</template>
<script>

    export default {
        el:'#shopping-cart',
        data(){
            return{
                productList: [
                    {
                        src:'../../static/imgs/goods/01.jpg',
                        'pro_name': '标准大床房 [特惠]',//床型
                        'pro_btime': '',//入住时间
                        'pro_etime': '',//离店时间
                        'pro_etype': '不含早',//是否含早类型
                        'pro_btype': "30m²",//床的大小
                        'pro_cancel': '不可取消',//是否可取消
                        'pro_num': 1,//数量
                        'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
                        'pro_price': 250,//单价
                        'pro_minutes':2,//几分钟前购买了
                        count1:14

                    },
                    {
                        src:'../../static/imgs/goods/05.jpg',
                        'pro_name': '全家旅行房',//床型
                        'pro_btime': '',//入住时间
                        'pro_etime': '',//离店时间
                        'pro_etype': '不含早',//是否含早类型
                        'pro_btype': "30m²",//床的大小
                        'pro_cancel': '不可取消',//是否可取消
                        'pro_num': '2',//数量
                        'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
                        'pro_price': 300,//单价
                        'pro_minutes':7,
                        count1:1
                    },
                    {
                        src:"../../static/imgs/goods/02.jpg",
                        'pro_name': '标准商务房',//床型
                        'pro_btime': '',//入住时间
                        'pro_etime': '',//离店时间
                        'pro_etype': '不含早',//是否含早类型
                        'pro_btype': "20-25m²",//床的大小
                        'pro_cancel': '可取消',//是否可取消
                        'pro_num': 3,//数量
                        'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
                        'pro_price': 90,//单价
                        'pro_minutes':12,
                        count1:2
                    },
                    {
                        src:"../../static/imgs/goods/03.jpg",'pro_name': '标准商务房',//床型
                        'pro_btime': '',//入住时间
                        'pro_etime': '',//离店时间
                        'pro_etype': '不含早',//是否含早类型
                        'pro_btype': "20-25m²",//床的大小
                        'pro_cancel': '可取消',//是否可取消
                        'pro_num': 4,//数量
                        'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
                        'pro_price': 180,//单价
                        'pro_minutes':12,
                        count1:12
                    },
                    {
                        src:"../../static/imgs/goods/04.jpg",'pro_name': '全家旅行房',//床型
                        'pro_btime': '',//入住时间
                        'pro_etime': '',//离店时间
                        'pro_etype': '不含早',//是否含早类型
                        'pro_btype': "30m²",//床的大小
                        'pro_cancel': '不可取消',//是否可取消
                        'pro_num': 5,//数量
                        'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
                        'pro_price': 220,//单价
                        'pro_minutes':3,
                        count1:15
                    },
                    {
                        src:"../../static/imgs/goods/01.jpg",'pro_name': '标准商务房',//床型
                        'pro_btime': '',//入住时间
                        'pro_etime': '',//离店时间
                        'pro_etype': '不含早',//是否含早类型
                        'pro_btype': "20-25m²",//床的大小
                        'pro_cancel': '可取消',//是否可取消
                        'pro_num': 6,//数量
                        'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
                        'pro_price': 300,//单价
                        'pro_minutes':15,
                        count1:30
                    },
                    {
                        src:"../../static/imgs/goods/01.jpg",'pro_name': '全家旅行房',//床型
                        'pro_btime': '',//入住时间
                        'pro_etime': '',//离店时间
                        'pro_etype': '不含早',//是否含早类型
                        'pro_btype': "30m²",//床的大小
                        'pro_cancel': '不可取消',//是否可取消
                        'pro_num': 7,//数量
                        'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
                        'pro_price': 400,//单价
                        'pro_minutes':3,
                        count1:3
                    }
                ]
            }
        },
        methods: {
            addCart(id, price, btime, etime,index,img) {
                this.$router.push({
                    path:'/shopcar',
                    name:'shopcar',
                    params:{
                        'pro_name':id,
                       'pro_price':price,
                        'pro_btime':btime,
                        'pro_etime':etime,
                        'pro_num':index,
                        src:img
                    }
                })
            },
            getParams1:function() {
                // 取到路由带过来的参数
                var routerParams = this.$route.params.bv1;
                // 将数据放在当前组件的数据内
                for (var i=0;i<this.productList.length;i++){
                this.productList[i].pro_btime = routerParams;}
                routerParams = this.$route.params.bv2;
                for (var j=0;j<this.productList.length;j++){

                // 将数据放在当前组件的数据内
                this.productList[j].pro_etime = routerParams;}
            }
        },
        watch:{
            '$route': 'getParams1'
        }
    }
</script>
<style scoped>
    button{
        color: darkred;
    }
    button:hover{
        background-color: darkred;
        color: #fff;
    }
.mui-table-view.mui-grid-view .mui-table-view-cell > a:not(.mui-btn) {
    margin: 0;
    padding: 0;
    border: 1px solid #5c5c5c;
    box-shadow: 0 0 4px #666;
}

.sell > span {
    float: left;
    color: red;
    text-align: left;
}

.detail >.hot {
    float: left;
    text-align: left;
    font-size: 13px;
}

.detail >.count {
    float: right;
    text-align: right;
    font-size: 13px;
}

/*去除浮动*/
.detail {
    overflow: hidden;
}

.desc {
    color: rgba(95, 95, 95, 0.9 );
    background-color: rgba(10, 0.7, 0.9, 0.2);
}
.mui-table-view.mui-grid-view .mui-table-view-cell .mui-media-object {
    height: 150px;
}
.mui-table-view.mui-grid-view {
    padding-bottom: 60px;
}
</style>
