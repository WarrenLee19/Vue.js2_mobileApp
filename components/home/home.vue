<template>
	<!-- 轮播图 -->
	<div>
		<div class="swipe">
            <mt-swipe :auto="2000">
                <mt-swipe-item v-for="(img,index) in bannerData" :key="index">
                	<a :href="img.url">
                		<img :src="img.src" alt="">
                	</a>
                </mt-swipe-item>
            </mt-swipe>
        </div>

        <div>
        	<ul class="mui-table-view mui-grid-view mui-grid-9">
	            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
	            	<!-- vue-router跳转 -->
	            	<router-link :to="{name:'newsList'}">
	                    <span class="mui-icon mui-icon-home"></span>
	                    <div class="mui-media-body">新闻资讯</div>
                    </router-link>
                </li>
	            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
	            	<router-link :to="{name:'hotelServe'}">
	                    <span class="mui-icon mui-icon-email"></span>
	                    <div class="mui-media-body">酒店服务</div>
	                </router-link>
                </li>
				<li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
					<router-link :to="{name:'hotelTimer'}">
						<span class="mui-icon mui-icon-location"></span>
						<div class="mui-media-body">住宿时间</div>
					</router-link>
				</li>
	            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
	            	<router-link :to="{name:'goodsList'}">
	                    <span class="mui-icon mui-icon-chatbubble"></span>
	                    <div class="mui-media-body">预订酒店</div>
	                </router-link>
                </li>

	            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
	            	<a href="#">
	                    <span class="mui-icon mui-icon-search"></span>
	                    <div class="mui-media-body">搜索查询</div>
	                </a>
                </li>
	            <li class="mui-table-view-cell mui-media mui-col-xs-4 mui-col-sm-3">
	            	<a href="#">
	                    <span class="mui-icon mui-icon-phone"></span>
	                    <div class="mui-media-body">联系我们</div>
	                </a>
                </li>
	        </ul> 
        </div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				bannerData: [],
				// 轮播图数据
			}
		},
		created(){ // 组件初始化时期请求数据
			this.$ajax.get('/lunbo').then((res)=>{
				this.bannerData = res.data.bannerSrc; // 拿到数据
			});
		}
	}
</script>

<style scoped>

	.swipe {
		height: 190px;
	}
	.mui-table-view.mui-grid-view.mui-grid-9 {
		border: none;
		background: #fff;
	}
	.mui-table-view.mui-grid-view.mui-grid-9:after {
		height: 0;
	}
	.mui-table-view-cell.mui-media.mui-col-xs-4.mui-col-sm-3 {
		border: none;
		background-color: #fff;
	}
	.mui-icon {
		width: 50px;
		height: 50px;
	}
	.mui-icon-home:before,
	.mui-icon-email:before,
	.mui-icon-chatbubble:before,
	.mui-icon-location:before,
	.mui-icon-search:before,
	.mui-icon-phone:before {
		content: '';
	}
	.mui-icon-home {
		background: url('../../static/imgs/home/news.png') no-repeat center;
		background-size: 100%;
	}
	.mui-icon-email {
		background: url('../../static/imgs/home/picShare.png') no-repeat center;
		background-size: 100%;
	}
	.mui-icon-chatbubble {
		background: url('../../static/imgs/home/goodShow.png') no-repeat center;
		background-size: 100%;
	}
	.mui-icon-location {
		background: url('../../static/imgs/home/feedback.png') no-repeat center;
		background-size: 100%;
	}
	.mui-icon-search {
		background: url('../../static/imgs/home/search.png') no-repeat center;
		background-size: 100%;
	}
	.mui-icon-phone {
		background: url('../../static/imgs/home/callme.png') no-repeat center;
		background-size: 100%;
	}

</style>