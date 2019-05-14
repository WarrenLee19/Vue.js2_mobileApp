<template>
    <!--操作步骤：分别填写入住和离开日期，再点击确定日期，最后点击提交-->
    <section class="l select-time">
        <p id="rent-time">xx酒店,请分别填写入住和离开日期，再点击确定日期，最后点击提交 <br> 入住日期：<button id="btn1" v-on:click="btnclick" >确定日期</button><input type="date" id="date1" v-model="bv1">&nbsp;&nbsp;&nbsp;离店时期：<button id="btn2" v-on:click="btnclick2">确定日期</button> <input type="date" id="date2" v-model="bv2">
            <button @click="addCart1(bv1,bv2)" style="margin-left: 200px;width: 80px;font-size: larger">&nbsp; 提交 &nbsp;</button></p>
        <div class="calendar-box clear"></div>
    </section>
</template>

<script>
    export default {
        name: "hotelTimer",
        data(){
            return {
                bv1:document.getElementById("date1").value,
                bv2:document.getElementById("date2").value

            }
        },
        methods:{
            btnclick:function () {
                var btn1=document.getElementById("btn1");
                var date1=document.getElementById('date1');

                var x = document.getElementById("date1").value;
                if(x===""){
                    return;
                }
                btn1.innerHTML=x;
                date1.style.display="none";

            },
            btnclick2:function () {
                var btn2=document.getElementById("btn2");
                var date2=document.getElementById("date2");
                var x = document.getElementById("date2").value;
                if(x===""){
                    return;
                }
                btn2.innerHTML=x;
                btn2.value=x;
                date2.style.display="none";

            },
            //传参至goodsList页面
            addCart1(bv11,bv22) {
                this.$router.push({
                    path:'/goodsList',
                    name:'goodsList',
                    params:{
                        bv1:bv11,
                        bv2:bv22
                    }
                })
            }
        }

    }
</script>

<style scoped>
    html,
    body {
        height: 100%;
    }

    .select-time {
        position: relative;
        top: 5px;
        left: 5px;
    }

    #rent-time {
        margin-left: 10px;
        padding-left: 45px;
        width: 500px;
        height: 55px;
        line-height: 53px;
        border: 1px solid #edeeed;
        cursor: pointer;
        background: url(../../HotelTime/images/index-date.png) no-repeat 18px 17px #fff;
        font-size: 16px;
        color: #666666;
    }


    button{
        line-height: 34px;
        margin-top: 10px;
        color: #e25a2a;
    }
    button:hover{
        line-height: 34px;
        margin-top: 10px;
        background-color: #e25a2a;
        color: #fff;
    }
</style>