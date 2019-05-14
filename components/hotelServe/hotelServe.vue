<template>
	<div class="tmpl">
        <!-- 引入返回导航 -->
        <div class="photo-header">
            <ul>
                <li v-for="item in category1" @click="mesg">
                    <a href="javascript:;">{{item.category2}}</a>
                </li>
            </ul>
        </div>
        <div class="photo-list">
            <ul>
                <li v-for="item in category">
                    <a>
                        <img :src="item.src" alt="">
                        <p>
                            <span>{{item.title}}</span>
                            <br>
                            <span>{{item.detail}}</span>
                        </p>
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
                category:[{
                    src:'../../static/imgs/goods/01.jpg',
                    title:123,
                    detail:321
                },{
                    src:'../../static/imgs/goods/01.jpg',
                    title:123,
                    detail:321
                },{
                    src:'../../static/imgs/goods/01.jpg',
                    title:123,
                    detail:321
                },{
                    src:'../../static/imgs/goods/01.jpg',
                    title:123,
                    detail:321
                }],
                category1:[{
                    category2:"按摩服务"
                },{
                    category2:"餐厅服务"
                },{
                    category2:"游戏服务"
                },{
                    category2:"健身服务"
                }]
            }
        },
        methods:{
		    mesg:function () {
                alert("今天没有开业");
            }
        }
	}
</script>

<style scoped>
	.photo-header li {
	    list-style: none;
	    display: inline-block;
	    margin-left: 10px;
	    height: 30px;
	}

	.photo-header ul {
	    /*强制不换行*/
	    white-space: nowrap;
	    overflow-x: auto;
	    padding-left: 0px;
	    margin: 5px;
	}

	/*下面的图片*/

	.photo-list li {
	    list-style: none;
	    position: relative;
	}

	.photo-list li img {
	    width: 100%;
	    height: 230px;
	    vertical-align: top;
	}

	.photo-list ul {
	    padding-left: 0;
	    margin: 0;
	    padding-bottom: 60px;
	}

	.photo-list p {
	    position: absolute;
	    bottom: 0;
	    color: white;
	    background-color: rgba(0, 0, 0, 0.3);
	    margin-bottom: 0;
	}

	.photo-list p span:nth-child(1) {
	    font-weight: bold;
	    font-size: 16px;
	}

</style>