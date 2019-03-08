<template>
    <div>
       <div class="choose_style">
       	  <span class="newSong" @click=changesingger  v-bind:class="{active:isActive }">
       	  	<p>新歌速递</p>
       	  </span>
       	   <span class="newablum" @click=changenewAblum  v-bind:class="{active:NActive }">
       	  	<p>新碟上架</p>
       	  </span>
       </div>
    </div>
</template> 
<script>
import Vue from 'vue'
export default{
	 mounted(){
  /*页面挂载获取cookie，如果存在username的cookie，则跳转到主页，不需登录*/
    Vue.http.get('/newapi/top/playlist?limit=10&order=new').then(response => {
      
      this.newList=response.body.result
    })
    Vue.http.get('/newapi/top/album?offset=0&limit=30').then(response => {
      
      this.newAblum=response.body.result
    })
   },
	data(){
		return{
			isActive:true,
		    NActive:false,
		    newList:[],
		    newAblum:[]
		}
	},
	methods:{
		changesingger(){
			isActive=true;
			NActive=false;
			console.log(isActive)
		},
		changenewAblum(){
			isActive=false;
			NActive=true;
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
</style>
