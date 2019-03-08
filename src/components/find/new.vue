<template>
    <div>
       <div class="choose_style">
       	  <span class="newSong item" @click=change(0)  v-bind:class="{active:isActive }">
       	  	<p>新歌速递</p>
       	  </span>
       	   <span class="newablum item" @click=change(1)  v-bind:class="{active:isActive }">
       	  	<p>新碟上架</p>
       	  </span>
       </div>
       	<p class="tittle">全部</p>
       <div class="Listitem">
        	<div class="play-all" >
              <img src="../../assets/play2.png" alt="" @click="$store.commit('addAllSong',newList)"><span @click="$store.commit('addAllSong',newList)">播放全部</span>
            </div>
            <ul class="songlist">
	              <li class="item"  v-for="(value, key) in newList" @click="$store.commit('addSong', value.song)">
	                  <div style="width:7%">{{key + 1>=10?key + 1:"0"+(key+ 1)}}</div>
	                  <div style="width:8%;position:relative" class="play_hover"><img :src="value.song.album.picUrl" alt=""><img class="playlog" src="../../assets/player_log.svg" @click="$store.commit('addSong', value.song)" alt=""></div>
	                  <div style="width:30%">{{value.name}}</div>
	                  <div style="width:20%">{{value.song.artists[0].name}} {{value.song.artists[1]?"/ "+value.song.artists[1].name:""}}</div>
	                  <div style="width:20%">{{value.song.alias[0]}}</div>
	                  <div style="width:15%">{{value.song.duration | durationToTime}}</div>
	              </li>
        </ul>
       </div>
    </div>
</template> 
<script>
import playlist from 'deal/playlist.js'
import Vue from 'vue'
export default{
	 mounted(){
  /*页面挂载获取cookie，如果存在username的cookie，则跳转到主页，不需登录*/
    Vue.http.get('/newapi/personalized/newsong').then(response => {
      console.log(response.data.result,"新歌111" )
      console.log(response.data)
      this.newList=response.data.result

    })
    Vue.http.get('/newapi/top/album?offset=0&limit=30').then(response => {
      console.log(response.body,"新碟")
      this.newAblum=response.body.result
    })
   },
	data(){
		return{
			isActive:true,
		    NActive:false,
		    newList:[],
		    newAblum:[],
		    allnewList:[]
		    
		}
	},
	methods:{
		change(tagindex){
			var items=document.getElementsByClassName("item") 
			console.log(items)
			 for( var i=0 ;i<items.length;i++){
                  this.isActive = false;  
			 }
			  this.items[tabIndex].isActive = true;  
			  console.log(this.items[tabIndex])
		}

	}
	 
}
</script>
<style scoped>
    .active{
    	background-color: #888888;
    	color: #fff;
    }
    .choose_style{
    	margin-top: 20px;
    	height: 30px;
    	width:100%;
    	text-align: center;
    }
    .newSong,.newablum{
    	display: inline-block;
    	width: 80px;
    	height:30px;
    	line-height: 30px;
    }
    .newSong,.newablum>p{
		font-size: 12px;
    }
    .newSong{
    	border-top-left-radius:2em;
    	border-bottom-left-radius:2em;
    	border: 1px solid #dcdcdc;
    	border-right:none;
    }
    .newablum{
    	border-top-right-radius:2em;
		border-bottom-right-radius:2em;
    	border: 1px solid #dcdcdc;
    	border-left:none;
    }
    .tittle{
	padding: 10px;
	border-bottom: 1px solid #e1e1e2;
    }
    .Listitem{
    	margin-top: 15px;
    	border: 1px solid #e1e1e2;
    	height: 500px;
    }
    .play-all{
    width: 122px;
    border: 1px solid rgb(225,225,226);
    margin-right: 10px;
    padding: 2px 10px;
    margin-left: 10px;
    margin-top: 10px;
    font-size: 12px;
    border-radius: 5px;
    position: relative;
    cursor: pointer;
    height: 36px;
    line-height: 33px;
    margin-bottom: 10px
    }
    .play-all::before{
      background-image: url('../../assets/play2.png');
    }
    .add{
	  border-left: 1px solid rgb(225,225,226);
	  margin-left: 5px;
	  text-align: center;
	  font-size: 15px;
	  padding-left: 5px;
	}
	.play-all img{
		width: 22px;
		height: 22px;
		vertical-align: -11px;
		margin:5px; 
	}
	li{
  list-style: none;
}

li.head div{
  box-sizing: border-box;
  float: left;
  display: inline-block;
  height: 30px;
  line-height: 30px;
  text-align: left;
  font-size: 13px;
  color: rgb(102,102,102);
  text-indent: 10px;
  border: 1px rgb(225,225,226) solid;
}

li.item,
li.head{
  overflow: hidden;
}

li.item div{
  box-sizing: border-box;
  float: left;
  display: inline-block;
  line-height: 55px;
  height: 55px;
  text-align: left;
  font-size: 13px;
  color: rgb(102,102,102);
  text-indent: 12px;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}
li.item img{
	width: 100%;
	margin:10px 0; 
}
li.item:nth-child(odd){
  background-color: rgb(245,245,247);
}

li.item:hover{
  background-color: rgb(236,237,238);
}
.playlog{
	position: absolute;
    top: 10px;
    left: 21px;
    width: 29px !important;
    border-radius: 50%;
}
.playlog:hover{
	background: rgba(83, 75, 75, 0.4 );
}
</style>
