<template>
	<div id="list" name="list">
		<dl>
      <dt><span>推荐</span></dt>
      <router-link to="/find/recommend"><dd :class="{choosed: choosed == 'find'}"><span><img class="icon" src="../assets/music.png"> 发现音乐</span></dd></router-link>  
      <router-link to="/personal/"><dd to-link :class="{choosed: choosed == 'personal'}"><span><img class="icon" src="../assets/fm.png">私人FM</span></dd></router-link>  
      <router-link to="/mv/"><dd :class="{choosed: choosed == 'mv'}"><span><img class="icon" src="../assets/mv.png">MV</span></dd></router-link>  
      <router-link to="/friend/"><dd :class="{choosed: choosed == 'friend'}"><span><img class="icon" src="../assets/friend.png">朋友</span></dd></router-link>  
      <dt><span>我的音乐</span></dt>
      <router-link to="/local/"><dd :class="{choosed: choosed == 'local'}"><span><img class="icon" src="../assets/local_music.png">本地音乐</span></dd></router-link>  
      <router-link to="/download/"><dd :class="{choosed: choosed == 'download'}"><span><img class="icon" src="../assets/download.png">下载管理</span></dd></router-link>  
       
      <div v-if="showlist">
          <router-link to="/cloud/"><dd :class="{choosed: choosed == 'cloud'}"><span><img class="icon" src="../assets/cloud.png">我的音乐云盘</span></dd></router-link>  
          <router-link to="/singer/"><dd :class="{choosed: choosed == 'singer'}"><span><img class="icon" src="../assets/singer.png">我的歌手</span></dd></router-link>  
          <router-link to="/station/"><dd :class="{choosed: choosed == 'station'}"><span><img class="icon" src="../assets/station.png">我的电台</span></dd></router-link>
          <dt><span>创建的歌单</span></dt>
          <router-link v-for="(value, key) in createList" :to="'/playlist/'+value.id"><dd :class="{choosed: choosed == value.id}"><span><img class="icon" src="../assets/list.png"/>{{value.name.indexOf("喜欢的音乐")>-1?"我喜欢的音乐":value.name}}</span></dd></router-link>
           <dt><span>收藏的歌单</span></dt>
          <router-link v-for="(value, key) in collectionList" :to="'/playlist/'+value.id"><dd :class="{choosed: choosed == value.id}"><span><img class="icon" src="../assets/list.png">{{value.name}}</span></dd></router-link>
      </div>
      <div v-else>
         <router-link to="/download/"><dd :class="{choosed: choosed == 'download'}"><span><img class="icon" src="../assets/heart.png">我喜欢的音乐</span></dd></router-link>  
      </div>
    </dl>
	</div>
</template>
<script >
import { setCookie,getCookie,delCookie } from 'assets/js/cookie.js'
import Vue from 'vue'
 
export default {
  name: 'list',
  props: ['choosed'],
  mounted(){
/*页面挂载获取保存的cookie值，渲染到页面上*/
            let userid = getCookie('userid')
            if(userid){
                this.showlist=true
                Vue.http.get('newapi/user/playlist?'+'uid='+userid).then(res => {
                  if(res.data.playlist.length){
                      for(var i=0;i<res.data.playlist.length;i++){
                        if(res.data.playlist[i].creator.userId==userid){
                          this.createList.push(res.data.playlist[i])
                        }else{
                          this.collectionList.push(res.data.playlist[i])
                        }
                     }
                  }
                
              }) 
               /*Vue.http.get('newapi//user/record?'+'uid='+userid+"&type=1").then(res => {
                   console.log(res)
                
              })   */
            }
                   
        },
  data () {
    return {
      app: '网易云音乐',
      showlist:false,
      createList:[],
      collectionList:[]
    }
  }
}
</script>
<style scoped>
#list{
	height: 100%;
  background-color: rgb(245,245,247);
  overflow-y: scroll;
  border-right: 1px solid rgb(225,225,226)
}

dt,dd{
  height: 30px;
  line-height: 30px;
  font-family: microsoft yahei;
  position: relative;
  font-size: 14px;
}

dd{
  text-indent: 20px;
  font-size: 13px;
  opacity: 0.8;
  color: black;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

dd:hover{
  opacity: 1.0;
  cursor: pointer;
}

dt{
  text-indent: 10px;
  color: rgb(125,125,125);
}

.icon{
  width: 20px;
  height: 20px;
  vertical-align: top;
  margin-right: 10px;
  margin-top: 5px;
}

.choosed{
  background-color: rgb(230,231,234);
  opacity: 1.0;
  color: black;
}

.choosed:before{
  position: absolute;
  left: 0px;
  top: 0px;
  display: inline-block;
  content: ' ';
  width:5px;
  height: 30px;
  background-color: rgb(198,47,47);
}


/*定义滚动条高宽及背景 高宽分别对应横竖滚动条的尺寸*/
::-webkit-scrollbar {
  width: 7px;
  background-color: #F5F5F5;
}
/*定义滚动条轨道 内阴影+圆角*/
::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, 0);
  border-radius: 10px;
  background-color: rgb(245,245,247);
}
/*定义滑块 内阴影+圆角*/
::-webkit-scrollbar-thumb {
  border-radius: 10px;
  -webkit-box-shadow: inset 0 0 6px rgb(225,225,226);
  background-color: rgb(225,225,226);
}
</style>
