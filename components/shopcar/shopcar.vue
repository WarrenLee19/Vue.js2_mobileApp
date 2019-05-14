<template>
    <!--到此购物车页面时，需要点击“更新购物车”，为了录入酒店订单信息-->
	<div class="page-shopping-cart" id="shopping-cart">
		<h4 class="cart-title">购物车<button class="update1" @click="go1">&nbsp;<span class="mui-icon mui-icon-redo"></span>继续购物&nbsp;</button><button class="update1" @click="getParams">&nbsp;<span class="mui-icon icon-gouwuchekong"></span>&nbsp;更新购物车&nbsp;</button></h4>
		<div class="cart-product-title clearfix">
			<div class="td-check fl">
				<span class="check-span fl check-all" :class="{'check-true':isSelectAll}" @click="selectOrNot(isSelectAll)"></span>全选</div>
			<div class="td-product fl">商品</div>
			<div class="td-num fl">数量</div>
			<div class="td-price fl">单价(元)</div>
			<div class="td-total fl">金额(元)</div>
			<div class="td-do fl">操作</div>
		</div>
		<div class="cart-product clearfix">
			<table>
				<tbody>
				<!-- 加入index用于删除的时候判断索引 -->
				<tr v-for="(item,index) in productList">
					<td class="td-check"><span class="check-span" :class="{'check-true':item.select}" @click="item.select=!item.select"></span></td>
					<td class="td-product"><img v-bind:src="item.src" style="width:120px; height: 93px" alt="商品">
						<div class="product-info">
							<p id="namestyle">{{item.pro_name}}</p>
							<p>入住时间：{{item.pro_btime}}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	离店时间：{{item.pro_etime}}</p>
							<p>{{item.pro_etype}}&nbsp;&nbsp;&nbsp;&nbsp;{{item.pro_btype}}</p>
							<p>{{item.pro_cancel}}</p>
						</div>
						<div class="clearfix"></div>
					</td>
					<td class="td-num">
						<div class="product-num">
							<a href="javascript:" class="num-reduce num-do fl" @click="item.pro_num>0?item.pro_num--:''"><span></span>-</a>
							<input type="text" class="num-input" value="3" v-model="item.pro_num">
							<a href="javascript:" class="num-add num-do fr" @click="item.pro_num++"><span></span>+</a>
						</div>
					</td>
					<td class="td-price">
						<p class="red-text">￥<span class="price-text">{{item.pro_price}}</span></p>
					</td>
					<td class="td-total">
						<p class="red-text">￥<span class="total-text">{{item.pro_num*item.pro_price}}</span>.00</p>
					</td>
					<td class="td-do"><a href="javascript:" class="product-delect" @click="deleteOne(index)">删除</a></td>
				</tr>
				</tbody>
			</table>
		</div>

		<div class="cart-product-info">
			<a class="delect-product" href="javascript:" @click="deleteSome"><span id="shop11"></span>删除所选商品</a>
			<p class="fr product-total">￥<span>{{total.totalPrice}}</span></p>
			<p class="fr check-num"><span>{{total.totalNum}}</span>件商品总计（不含运费）：</p>
			<a class="btn-buy fr" href="javascript:">去结算</a>
		</div>
		<div class="cart-worder clearfix">
			<a href="javascript:;" class="choose-worder fl"><span></span>绑定我的账号</a>
			<div class="worker-info fl">
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		el:'#shopping-cart',
		data(){
			return{
				productList: [
				{
					src:'',
					'pro_name': '',//床型
					'pro_btime': '',//入住时间
					'pro_etime': '',//离店时间
					'pro_etype': '不含早',//是否含早类型
					'pro_btype': "30m²",//床的大小
					'pro_cancel': '不可取消',//是否可取消
					'pro_num': 1,//数量
					'pro_img': '../../static/imgs/goods/01.jpg',//图片链接
					'pro_price':''//单价
				}
			]
			}
		},
		computed: {
			// 检测是否全选
			isSelectAll:function(){
				if(this.productList.length <= 0){
					return false;
				}
					return this.productList.every(function(val){
					return val.select;
				})
			},
			total: function(){
				var _pro = this.productList.filter(function(val){return val.select});
				var totalPrice = 0;
				for(var i = 0; i < _pro.length; i++){
					totalPrice += _pro[i].pro_num * _pro[i].pro_price;
				}
				return {totalNum:_pro.length,totalPrice:totalPrice}
			}
		},
		methods: {
			// 全选与取消全选
			selectOrNot: function (_select) {
				for (var i = 0; i < this.productList.length; i++) {
					this.productList[i].select = !_select;
				}
			},
			// 单个删除
			deleteOne: function (index) {
				this.productList.splice(index, 1);
			},
			// 批量删除
			deleteSome: function () {

				this.productList = this.productList.filter(function (val) {
					return !val.select
				})
			},
			//继续购物路由回到goodList页面
			go1:function(){
				this.$router.push('/hotelTimer');
			},
			getParams:function() {
				// 取到路由带过来的参数

				var routerParams = this.$route.params.pro_name;
				// 将数据放在当前组件的数据内
				this.productList[0].pro_name = routerParams;
				 routerParams = this.$route.params.pro_price;
				// 将数据放在当前组件的数据内
				this.productList[0].pro_price = routerParams;
				 routerParams = this.$route.params.pro_btime;
				// 将数据放在当前组件的数据内
				this.productList[0].pro_btime = routerParams;
				 routerParams = this.$route.params.pro_etime;
				// 将数据放在当前组件的数据内
				this.productList[0].pro_etime = routerParams;
				 routerParams = this.$route.params.src;
				// 将数据放在当前组件的数据内
				this.productList[0].src = routerParams;
			}
			},
			watch: {
				// 监测路由变化,只要变化了就调用获取路由参数方法将数据存储本组件即可
				'$route': 'getParams'
			},
			mounted: function () {
				var _this = this;
				this.productList.map(function (item) {
					_this.$set(item, 'select', true);
				})
			}
	}
</script>

<style>
	.fl {
		float: left;
	}
	.fr {
		float: right;
	}
	blockquote, body, dd, div, dl, dt, fieldset, form, h1, h2, h3, h4, h5, h6, img, input, li, ol, p, table, td, textarea, th, ul {
		margin: 0;
		padding: 0;
	}
	.clearfix {
		zoom: 1;
	}
	.clearfix:after {
		clear: both;
	}
	.clearfix:after {
		content: '.';
		display: block;
		overflow: hidden;
		visibility: hidden;
		font-size: 0;
		line-height: 0;
		width: 0;
		height: 0;
	}
	a {
		text-decoration: none;
		color: #333;
	}
	img {
		vertical-align: middle;
	}
	.page-shopping-cart {
		width: 520px;
		margin: 0px auto;
		margin-bottom: 40px;
		font-size: 12px;
		border: 1px solid #e3e3e3;
		border-top: 3px solid #e76c12;
	}
	.page-shopping-cart .cart-title {
		color: #e76c12;
		font-size: 16px;
		text-align: left;
		padding-left: 20px;
		line-height: 48px;
	}
	.page-shopping-cart .red-text {
		color: #e76c12;
	}
	.page-shopping-cart .check-span {
		display: block;
		width: 24px;
		height: 20px;
		background: url("shopping_cart.png") no-repeat 0px -29px;
	}
	.page-shopping-cart .check-span.check-true {
		background: url("shopping_cart.png") no-repeat 0 0px;
	}
	.page-shopping-cart .td-check {
		width: 70px;
	}
	.page-shopping-cart .td-product {
		width: 130px;
	}
	.page-shopping-cart .td-num, .page-shopping-cart .td-price {
		width: 100px;
	}
	 .page-shopping-cart .td-total{
		width: 60px;
	}
	.page-shopping-cart .td-do {
		width: 30px;
	}
	.page-shopping-cart .cart-product-title {
		text-align: center;
		height: 35px;
		line-height: 35px;
		padding: 0 10px;
		background: #f7f7f7;
		border-top: 1px solid #e76c12;
		border-bottom: 1px solid #e76c12;
	}
	.page-shopping-cart .cart-product-title .td-product {
		text-align: center;
		font-size: 11px;
	}
	.page-shopping-cart .cart-product-title .td-check {
		text-align: left;
	}
	.page-shopping-cart .cart-product-title .td-check .check-span {
		margin: 9px 6px 0 0;
	}
	.page-shopping-cart .cart-product {
		padding: 0 15px;
		text-align: center;
	}
	.page-shopping-cart .cart-product table {
		width: 100%;
		text-align: center;
		font-size: 11px;
	}
	.page-shopping-cart .cart-product table td {
		padding: 10px 0;
	}
	.page-shopping-cart .cart-product table tr {
		border-bottom: 1px dashed #e3e3e3;
	}
	.page-shopping-cart .cart-product table tr:last-child {
		border-bottom: none;
	}
	.page-shopping-cart .cart-product table .product-num {
		border: 1px solid #e3e3e3;
		display: inline-block;
		text-align: center;
	}
	.page-shopping-cart .cart-product table .product-num .num-do {
		width: 24px;
		height: 28px;
		display: block;
		background: #f7f7f7;
	}
	.page-shopping-cart .cart-product table .product-num .num-reduce span {

		display: block;

		margin: 6px auto 0 auto;
	}

	.page-shopping-cart .cart-product table .product-num .num-add span {

		display: block;

		margin: 6px auto 0 auto;
	}

	.page-shopping-cart .cart-product table .product-num .num-input {
		width: 40px;
		height: 10px;
		line-height: 10px;
		border: none;
		text-align: center;
	}
	.page-shopping-cart .cart-product table .td-product {
		text-align: left;
		font-size: 12px;
		line-height: 20px;
	}
	.page-shopping-cart .cart-product table .td-product img {
		border: 1px solid #e3e3e3;
		margin-right: 10px;
	}
	.page-shopping-cart .cart-product table .td-product .product-info {
		display: inline-block;
		vertical-align: middle;

	}
	.page-shopping-cart .cart-product table .td-product .product-info p{
		font-size: 12px;

	}
	.page-shopping-cart .cart-product table .td-do {
		font-size: 12px;
	}
	.page-shopping-cart .cart-product-info {
		height: 45px;
		line-height: 45px;
		background: #f7f7f7;
		padding-left: 15px;
	}
	.page-shopping-cart .cart-product-info .delect-product {
		color: #666;
	}
	.page-shopping-cart .cart-product-info .delect-product span {
		display: inline-block;
		vertical-align: top;
		margin: 10px 8px 0 0;
		width: 23px;
		height: 25px;
		background: url("shopping_cart.png") no-repeat 0 0;
	}
	.page-shopping-cart .cart-product-info .product-total {
		font-size: 14px;
		color: #e94826;
	}
	.page-shopping-cart .cart-product-info .product-total span {
		font-size: 20px;
	}
	.page-shopping-cart .cart-product-info .check-num {
		color: #333;
	}
	.page-shopping-cart .cart-product-info .check-num span {
		color: #e94826;
	}
	.page-shopping-cart .cart-product-info .keep-shopping {
		color: #666;
		line-height: 45px;


	}

	.page-shopping-cart .cart-product-info .btn-buy {
		height: 45px;
		color: #fff;
		font-size: 16px;
		display: block;
		width: 110px;
		background: #ff7700;
		text-align: center;
		margin-left: 30px;
	}
	.page-shopping-cart .cart-worder {
		padding: 20px;
	}
	.page-shopping-cart .cart-worder .choose-worder {
		color: #fff;
		display: block;
		background: #39e;
		width: 130px;
		height: 40px;
		line-height: 40px;
		border-radius: 4px;
		text-align: center;
		margin-right: 20px;
	}
	.page-shopping-cart .cart-worder .choose-worder span {
		display: inline-block;
		vertical-align: top;
		margin: 9px 10px 0 0;
		width: 22px;
		height: 22px;
		background: url("shopping_cart.png") no-repeat 0 0;
	}
	.page-shopping-cart .cart-worder .worker-info {
		color: #666;
	}
	.page-shopping-cart .cart-worder .worker-info img {
		border-radius: 100%;
		margin-right: 10px;
	}
	.page-shopping-cart .cart-worder .worker-info span {
		color: #000;
	}
	.choose-worker-box {
		width: 620px;
		background: #fff;
	}
	.choose-worker-box .box-title {
		height: 40px;
		line-height: 40px;
		background: #F7F7F7;
		text-align: center;
		position: relative;
		font-size: 14px;
	}
	.choose-worker-box .box-title a {
		display: block;
		position: absolute;
		top: 15px;
		right: 16px;
		width: 10px;
		height: 10px;
		background: url("shopping_cart.png") no-repeat -22px 0;
	}
	.choose-worker-box .box-title a:hover {
		background: url("shopping_cart.png") no-repeat 0px 0px;
	}
	.choose-worker-box .worker-list {
		padding-top: 30px;
		height: 134px;
		overflow-y: auto;
	}
	.choose-worker-box .worker-list li {
		float: left;
		width: 25%;
		text-align: center;
		margin-bottom: 30px;
	}
	.choose-worker-box .worker-list li p {
		margin-top: 8px;
	}
	.choose-worker-box .worker-list li.cur a {
		color: #f70;
	}
	.choose-worker-box .worker-list li.cur a img {
		border: 1px solid #f70;
	}
	.choose-worker-box .worker-list li a:hover {
		color: #f70;
	}
	.choose-worker-box .worker-list li a:hover img {
		border: 1px solid #f70;
	}
	.choose-worker-box .worker-list li img {
		border: 1px solid #fff;
		border-radius: 100%;
	}
	#namestyle{
		color: #222222;
		font-size: 13px;
	}
	.update1{
		font-size: 16px;
		float: right;
		margin: 12px 10px 0 0;
		border: 2px solid #e94826;
		border-radius: 3%;
		color: #e94826;
	}
	.update1:hover{
		background-color: #e94826;
		color: #fff;
	}
</style>



