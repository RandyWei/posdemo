<template>
    <div class="left-nav">
        <ul>
            <li>
                <i class="iconfont icon-payment" />
                <div>收银</div>
            </li>
             <li>
                <i class="iconfont icon-home" />
                <div>店铺</div>
            </li>
             <li>
                <i class="iconfont icon-shopping" />
                <div>商品</div>
            </li>
             <li>
                <i class="iconfont icon-nickname" />
                <div>会员</div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {

}
</script>

<style>
.left-nav{
    height: 100%;
    color: #fff;
    font-size: 10px;
    background-color: #1d8ce0;
    float: left;
    width: 5%;
}
.iconfont{
    font-size: 40px;
}
.left-nav ul{
    padding: 0;
    margin: 0;

}
.left-nav li{
    list-style: none;
    text-align: center;
    border-bottom: 1px solid #20a0ff;
    padding: 10px;
}

.left-nav li div{
    font-size: 14px;
}
</style>
