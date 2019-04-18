<template>
    <div class="left-nav">
        <ul>
            <li>
                <i class="icon iconfont icon-goumai"></i>
                <div>收银</div>
            </li>
            <li>
                <i class="icon iconfont icon-dianpu"></i>
                <div>店铺</div>
            </li>
            <li>
                <i class="icon iconfont icon-hanbao"></i>
                <div>商品</div>
            </li>
            <li>
                <i class="icon iconfont icon-huiyuanqia"></i>
                <div>会员</div>
            </li>
            <li>
                <i class="icon iconfont icon-zuanshi"></i>
                <div>统计</div>
            </li>
            <li>
                <i class="icon iconfont icon-gongnengjianyi"></i>
                <div>设置</div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'leftNav',
    data() {
        return {
            
        }
    }
}
</script>

<style>
.left-nav {
    float: left;
    width: 6%;
    min-width: 28px;
    height: 100%;
    background-color: #1D8CE0;
}
.left-nav ul,li {
    list-style: none;
    margin: 0;
    padding: 0;
}
.left-nav li {
    font-size: 14px;
    color: #fff;
    text-align: center;
    width: 100%;
    height: 60px;
    padding-top: 14px;
    border-bottom: 1px solid #20a0ff;
    cursor: pointer;
}
.iconfont {
    font-size: 24px;
}
</style>
