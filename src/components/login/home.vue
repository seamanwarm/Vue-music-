	<template >
		<div>
			<div class="auto-1524643244651 m-layer z-show" style="top: 140px;left: 558px;">
				<div class="zbar" id="auto-id-0OdDVDDB5oId8uFy">
					<div class="zttl f-thide">手机号登录</div>
				</div>
				<div class="zcnt">
					<div class="lyct lyct-1" id="auto-id-b2ch04qrFrPoVozP">
						<div class="n-log2 n-log2-1 f-cb">
							<div class="u-main">
								<div class="u-plt" style=" background: url(static/img/platform.png) no-repeat 13px 0; "></div>
								<div class="f-mgt10">
									<router-link to="/loginphone/"><a href="javascript:;" class="u-btn2 u-btn2-2" data-action="login" data-type="mobile" ><i>手机号登录</i></a></router-link>
								</div>
								<div class="f-mgt10">
								<a href="javascript:;" class="u-btn2 u-btn2-1" data-action="reg"><i>注　册</i></a>
								</div>
							</div>
							<div class="u-alt">
								<ul>
									<li><a href="http://music.163.com/api/sns/authorize?snsType=10&amp;clientType=web2&amp;callbackType=Login&amp;forcelogin=true" target="_blank" data-action="login" data-type="thirdparty"><i class="u-mlg2 u-mlg2-wx"></i>微信登录</a></li>
									<li><a href="http://music.163.com/api/sns/authorize?snsType=5&amp;clientType=web2&amp;callbackType=Login&amp;forcelogin=true" target="_blank" data-action="login" data-type="thirdparty"><i class="u-mlg2 u-mlg2-qq"></i>QQ登录</a></li>
									<li><a href="http://music.163.com/api/sns/authorize?snsType=2&amp;clientType=web2&amp;callbackType=Login&amp;forcelogin=true" target="_blank" data-action="login" data-type="thirdparty"><i class="u-mlg2 u-mlg2-sn"></i>微博登录</a></li>
									<li><a href="javascript:;" data-action="login" data-type="netease"><i class="u-mlg2 u-mlg2-wy"></i>网易邮箱帐号登录</a></li>
								</ul>
							</div>
						</div>
					</div>
				</div>
				<span class="zcls" title="关闭窗体" id="auto-id-ma6ABDXluvm8gKDO">×</span>
			</div>
			<router-link to="/find/recommend/"><div class="auto-1524709305469 m-mask">&nbsp;</div></router-link>
		</div>
	</template>
<script>
export default{
	 
}
</script>
<style scoped>
em, i {
    font-style: normal;
    text-align: left;
    font-size: inherit;
}
.zbar {
    line-height: 30px;
    background: #8098E7;
    border-bottom: 1px solid #aaa;
}
    div.m-layer {
    position: absolute;
    z-index: 9998;
    width: 530px;
    border-radius: 4px;
    box-shadow: 0 5px 16px rgba(0,0,0,0.8);
    border: none;
    background: #fff;
	}
	div.m-layer .zbar {
    position: relative;
    z-index: 10;
    border-bottom: 1px solid rgb(168,40,40);
    border-radius: 4px 4px 0 0;
    background: rgb(168,40,40);
}
div.m-layer .zttl {
    padding-right: 45px;
    margin: 0;
    height: 38px;
    line-height: 38px;
    padding-left: 18px;
    border-radius: 3px 3px 0 0;
    font-weight: bold;
    font-size: 14px;
    color: #fff;
    background-position: 50% 0;
    
}
.f-thide {
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
    word-wrap: normal;
   
}
.zttl{
	text-align: left;
}
.div.m-layer .lyct-1 {
    padding: 0;
}
.n-log2-1 {
    padding: 40px 0 39px;
}
.n-log2 .u-main {
    float: left;
    width: 306px;
    padding: 0 35px 3px 40px;
    border-right: 1px dotted #ccc;
}
.n-log2 .u-alt {
    float: left;
    padding: 3px 0 3px 39px;
    margin-top: -15px;
}
.n-log2 .u-main .u-plt {
    height: 120px;
    
}
.f-mgt10 {
    margin-top: 10px;
}
.u-btn2, .u-btn2 i, .u-btn2 .icn, .u-btni, .u-btni i, .u-tag, .u-tag i, .u-btni-addply .ply {
   /*  background: url("../static/web2/img/button2.png") no-repeat 0 9999px; */
}
.u-btn2, .u-btn2 i {
    display: inline-block;
    height: 31px;
    line-height: 31px;
    overflow: hidden;
    vertical-align: top;
    text-align: center;
    cursor: pointer;
}
.u-btn2 {
    padding: 0 5px 0 0;
    white-space: nowrap;
}
.u-btn2, .u-btn2:hover {
    text-decoration: none;
}
.u-btn2-2 {
    color: #fff;
    background-position: right -428px;
}
.n-log2 .u-main .u-btn2 {
    width: 219px;
}
li, s {
    list-style: none;
}
.n-log2 .u-alt li {
    margin-top: 15px;
}
.n-log2 .u-alt li a {
    font-size: 12px;
    color: #333;
    line-height: 38px;
}
a, a *, .f-hand, .f-hand * {
    cursor: pointer;
}
.u-slg, .u-slg2, .u-slg3, .u-blg, .u-mlg, .u-mlg2, .u-errlg {
   /*  background: url("../../style/web2/img/logo.png") no-repeat 0 9999px; */
}
.u-slg, .u-slg2, .u-slg3, .u-blg, .u-mlg, .u-mlg2, .u-importlg, .u-errlg {
    display: inline-block;
    vertical-align: middle;
}
.u-mlg2 {
    width: 38px;
    height: 38px;
}
.u-mlg2-wx {
    background-position: -150px -670px;
}
.n-log2 .u-alt li .u-mlg2 {
    margin-right: 14px;
}
.u-mlg2-qq {
    background-position: -190px -670px;
}
.u-mlg2-sn {
    background-position: -231px -670px;
}
.u-mlg2-wy {
    background-position: -271px -670px;
}
div.m-layer .zbar, div.m-layer .zcls {
   /*  background: url("../../style/web2/img/layer/layer.png") no-repeat 0 9999px; */
   
}
div.m-layer .zcls {
    position: absolute;
    z-index: 20;
    top: 16px;
    right: 20px;
    width: 10px;
    height: 10px;
    overflow: hidden;
    text-indent: -9999px;
    cursor: pointer;
    background-position: 0 -95px;
}
.auto-1524709305469 {
    position: fixed;
    
    z-index: 100;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    width: 100%;
    height: 100%;
   
}
div.m-mask {
    z-index: 1001;
}
.u-btn2,  .u-btn2 .icn    {
    width: 100px;
    height: 30px;
    font-size: 18px;
    font-family: 微软雅黑;
    letter-spacing: 8px;
    padding-left: 12px;
    border-radius: 5px;
    background:#0c73c2;
    border: 1px solid #2576A8;
    box-shadow: 0 1px 2px #ecedee inset, 0 -1px 0 #316F96 inset;
    color: #fff;
     
}

.u-btn2,  .u-btn2 .icn  :hover {
    background:#2576a8;
   
}
.u-btn2-1,  .u-btn2-1 .icn    {
    width: 100px;
    height: 30px;
    font-size: 18px;
    font-family: 微软雅黑;
    letter-spacing: 8px;
    padding-left: 12px;
    border-radius: 5px;
    background:#f8f8f8;
    border: 1px solid #d0d0d0;
    box-shadow: 0 1px 2px #B8DCF1 inset, 0 -1px 0 #c3c3c3 inset;
    color: #282827;
    
}

.u-btn2-1,  .u-btn2-1 .icn  :hover {
    background:#f6f6f6;
   
}
</style>