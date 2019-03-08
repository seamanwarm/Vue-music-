
    <template >
        <div>
            <div class="auto-1524643244651 m-layer z-show" style="top: 140px;left: 558px;">
                <div class="zbar" id="auto-id-0OdDVDDB5oId8uFy">
                    <div class="zttl f-thide">登录</div>
                </div>
                <div class="zcnt">
                    <div class="lyct lyct-1" id="auto-id-zlnuB6XF2bQbJhWV">
                        <div class="n-log2 n-log2-2">
                            <div class="j-mob">
                                <div class="u-phonewrap" id="auto-id-h7k9HLOo9lWNblNp">
                                    <a class="current" href="javascript:;" data-action="toggle">
                                        <span class="j-code">+86</span>
                                        <span class="icn u-icn2 u-icn2-17"></span>
                                    </a>
                                    <div class="txtwrap">
                                        <input type="text" class="j-phone txt u-txt" placeholder="请输入手机号"  v-model="username"  id="auto-id-Lic85l9VCTtNAT5n">
                                    </div>
                                     <p v-show="showTishi">{{tishi}}</p>
                                 
                                </div>
                            </div>
                            <div class="f-mgt10">
                                <input type="password" class="j-pwd u-txt" placeholder="请输入密码"  v-model="password" id="auto-id-97D2wxUtJyzFNxus">
                            </div>
                            <div class="j-err u-err" style="display:none;"><i class="u-icn u-icn-25"></i><span></span></div>
                            <div class="f-mgt10">
                                <label class="s-fc3"><input type="checkbox" checked="checked" class="j-auto u-auto">自动登录</label>
                                <a href="#" class="f-fr s-fc3" data-action="forget">忘记密码？</a>
                            </div>
                            <div class="f-mgt20">
                                <a class="j-primary u-btn2 u-btn2-2" hidefocus="true" href="#"  v-on:click="login"><i>登　录</i></a>
                            </div>
                        </div>
                    <div class="js-btmbar n-loglink2 f-cb">
                        <a href="javascript:;" data-action="select" class="f-fl s-primary">&lt;&nbsp;&nbsp;其他登录方式</a>
                        <a href="javascript:;" data-action="reg" class="f-fr">没有帐号？免费注册&nbsp;&nbsp;&gt;</a>
                    </div>
                    </div>
                </div>
                <span class="zcls" title="关闭窗体" id="auto-id-ma6ABDXluvm8gKDO">×</span>
            </div>
            <router-link to="/find/recommend/"><div class="auto-1524709305469 m-mask">&nbsp;</div></router-link>
        </div>
    </template>
<script>
import {setCookie,getCookie} from '../../assets/js/cookie.js'
import Vue from 'vue'
export default{
    data(){
            return{
                showLogin: true,
                showRegister: false,
                showTishi: false,
                tishi: '',
                username: '',
                password: '',
                newUsername: '',
                newPassword: ''
            }
        },
     mounted(){
  /*页面挂载获取cookie，如果存在username的cookie，则跳转到主页，不需登录*/
    if(getCookie('userid')){
        Vue.http.get("/newapi/login/refresh").then(res=>{
            console.log(res)
            this.$router.push('/')
        })
        
     }
   },
  methods:{
    login(){
        if(this.username == "" || this.password == ""){
            alert("请输入用户名或密码")
        }else{
            let data = {'phone':this.username,'password':this.password}
            console.log(data)
            /*接口请求*/
           Vue.http.get(`/newapi/login/cellphone`+'?phone='+"+86"+this.username+'&password='+this.password).then(res => {
            /*接口被和谐了*/
            if(res.status==200){
                res.userid=81480966 
                    setCookie('userid',res.userid,new Date()+7); //设置用户编号
                    this.$router.push('/')
             }
             else{
                alert("密码错误")
             }
         })
      }
    }
  }  
}
</script>
<style scoped>
em, i {
    font-style: normal;
    text-align: left;
    font-size: inherit;
}
body, textarea, select, input, button {
    font-size: 12px;
    color: #333;
    font-family: Arial, Helvetica, sans-serif;
    -webkit-text-size-adjust: none;
}
body, textarea, select, input, button {
    font-size: 12px;
    color: #333;
    font-family: Arial, Helvetica, sans-serif;
    -webkit-text-size-adjust: none;
}
input:focus, textarea:focus, span:focus, a:focus, button:focus {
    outline: none;
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
.n-log2-2 .u-btn2-2, .n-log2-3 .u-btn2-2 {
    width: 215px;
}
.n-log2-2 .u-btn2-2 i, .n-log2-3 .u-btn2-2 i {
    width: 180px;
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
 
.u-slg, .u-slg2, .u-slg3, .u-blg, .u-mlg, .u-mlg2, .u-importlg, .u-errlg {
    display: inline-block;
    vertical-align: middle;
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
.n-log2-2 {
    padding: 30px 0 43px;
    width: 220px;
    margin: 0 auto;
}
.n-loglink2 {
    padding: 0 19px;
    height: 48px;
    border-top: 1px solid #c6c6c6;
    border-radius: 0 0 4px 4px;
    line-height: 48px;
    background-color: #f7f7f7;
}
.u-err {
    height: 17px;
    margin-top: 5px;
    line-height: 17px;
    color: #e33232;
}
.n-log2 .u-err {
    height: auto;
    line-height: 18px;
}
.f-mgt20 {
    margin-top: 20px;
}
.u-phonewrap {
    position: relative;
    height: 30px;
    margin: 0;
    border: 1px solid #cdcdcd;
    border-radius: 2px;
    z-index: 10;
}
.u-phonewrap .current {
    position: relative;
    float: left;
    display: block;
    height: 30px;
    line-height: 30px;
    padding: 0 18px 0 5px;
    border-right: 1px solid #cdcdcd;
}
.u-phonewrap .txtwrap {
    overflow: hidden;
}
.f-hide, .js-hide {
    display: none !important;
}
.u-phonewrap .options {
    position: absolute;
    top: 31px;
    left: -1px;
    width: 100%;
    height: 128px;
    border: 1px solid #cdcdcd;
    border-top: none;
    clear: both;
    background-color: #fff;
    overflow: auto;
}
.u-phonewrap .options .itm {
    height: 32px;
    line-height: 32px;
    color: #333;
    cursor: pointer;
    overflow: hidden;
}
.u-phonewrap .txt {
    display: block;
    padding: 5px 8px 5px;
    height: 28px;
    line-height: 28px;
    border: none;
}
.n-log2 .u-txt {
    width: 220px;
}
.s-fc3, a.s-fc3:hover {
    color: #666;

}
.s-fc3{
     font-size: 12px;
}
.n-log2 .u-auto {
    margin: 0 12px 0 0;
    vertical-align: middle;
}
.n-loglink2 {
    padding: 0 19px;
    height: 48px;
    border-top: 1px solid #c6c6c6;
    border-radius: 0 0 4px 4px;
    line-height: 48px;
    background-color: #f7f7f7;
}
.f-fl {
    float: left;
}
.n-loglink2 a {
    font-size: 12px;
    color: #999;
    text-decoration: none;
}
.n-loglink2 a.s-primary {
    color: #0c72c3;
}
.f-fr {
    float: right;
}
.n-loglink2 a {
    font-size: 12px;
    color: #999;
    text-decoration: none;
}
.n-loglink2 {
    padding: 0 19px;
    height: 48px;
    border-top: 1px solid #c6c6c6;
    border-radius: 0 0 4px 4px;
    line-height: 48px;
    background-color: #f7f7f7;
}
.u-txt {
    height: 30px;
    margin: 0;
    padding: 5px 6px 6px;
    border: 1px solid #cdcdcd;
    border-radius: 2px;
    line-height: 19px;
}
 
</style>
