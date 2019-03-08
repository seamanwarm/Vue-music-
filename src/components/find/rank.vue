<template>
    <div>
       <p class="tittle">官方榜单</p>
       <div class="items"  >
       	 	<div class="item-header">
       	 		<img :src="list1.coverImgUrl" alt="" >
       	 	</div>
       	 <div class="items-list" >
       	 	<ul >
              <li v-for="(value,key) in list1.tracks " class="item" @click="$store.commit('addSong', value)">
                  <div style="width:7%">{{key + 1}}</div>
                  <div style="width:8%"> </div>
                  <div style="width:45%; color:#333" >{{value.name}}</div>
                  <div style="width:30%">{{value.artists[0].name}}</div>
              </li>
            </ul>
       	 </div>
       </div>
       <div class="items center" >
       		<div class="item-header">
       	 		<img :src="list2.coverImgUrl" alt="" >
       	    </div>
       	    <div class="items-list" >
       	 	<ul >
              <li v-for="(value,key) in list2.tracks " class="item" @click="$store.commit('addSong', value)">
                  <div style="width:7%">{{key + 1}}</div>
                  <div style="width:8%"> </div>
                  <div style="width:45%; color:#333" >{{value.name}}</div>
                  <div style="width:30%">{{value.artists[0].name}}</div>
              </li>
            </ul>
       	 </div>
       </div>
       <div class="items">
       		<div class="item-header">
       	 		<img :src="list3.coverImgUrl" alt="" >
       	    </div>
       	    <div class="items-list" >
       	 	<ul >
              <li v-for="(value,key) in list3.tracks " class="item" @click="$store.commit('addSong', value)">
                  <div style="width:9%">{{key + 1}}</div>
                  <div style="width:8%"> </div>
                  <div style="width:45%; color:#333" >{{value.name}}</div>
                  <div style="width:30%">{{value.artists[0].name}}</div>
              </li>
            </ul>
       	 </div>
       </div>
              <div class="items"  >
       	 	<div class="item-header">
       	 		<img :src="list4.coverImgUrl" alt="" >
       	 	</div>
       	 <div class="items-list" >
       	 	<ul >
              <li v-for="(value,key) in list4.tracks " class="item" @click="$store.commit('addSong', value)">
                  <div style="width:7%">{{key + 1}}</div>
                  <div style="width:8%"> </div>
                  <div style="width:45%; color:#333" >{{value.name}}</div>
                  <div style="width:30%">{{value.artists[0].name}}</div>
              </li>
            </ul>
       	 </div>
       </div>
       <div class="items center" >
       		<div class="item-header">
       	 		<img :src="list5.coverImgUrl" alt="" >
       	    </div>
       	    <div class="items-list" >
       	 	<ul >
              <li v-for="(value,key) in list2.tracks " class="item" @click="$store.commit('addSong', value)">
                  <div style="width:7%">{{key + 1}}</div>
                  <div style="width:8%"> </div>
                  <div style="width:45%; color:#333" >{{value.name}}</div>
                  <div style="width:30%">{{value.artists[0].name}}</div>
              </li>
            </ul>
       	 </div>
       </div>
    </div>
</template> 
<script>
import Vue from 'vue'
export default{
  mounted(){
  /*页面挂载获取cookie，如果存在username的cookie，则跳转到主页，不需登录*/
    Vue.http.get('/newapi/top/list?idx=3').then(response => {
       
      this.list1=response.body.result
    })
    Vue.http.get('/newapi/top/list?idx=0').then(response => {
     
      this.list2=response.body.result
    })
    Vue.http.get('/newapi/top/list?idx=2').then(response => {
     
      this.list3=response.body.result
    })
    Vue.http.get('/newapi/top/list?idx=1').then(response => {
       
      this.list4=response.body.result
    })
    Vue.http.get('/newapi/top/list?idx=7').then(response => {
      
      this.list5=response.body.result
    })
   },
   data(){
   	 return{
   	 	list1:[],
   	 	list2:[],
   	 	list3:[],
   	 	list4:[],
   	 	list5:[]
   	 }
   },
}
</script>
<style scoped>
.tittle{
	padding: 10px;
	border-bottom: 1px solid #e1e1e2;
}
.items{
	margin-top: 4px;
	width: 32%;
	height: 403px;
	border: 1px solid #e1e1e2;
	float: left;
	overflow:hidden; 
	margin-bottom:14px;

}
.center{
	margin-right: 15px;
	margin-left: 15px;
}
.item-header{
	width:100%;
	height: 150px; 
}
.item-header>img{
   width: 100%;
   height: 150px;
}
.items-list ul{
	display: table;
	width: 100%;
}
.items-list ul li{
	width: 100%;
	 
	display: table;
}
.items-list div{
	float: left;
	overflow: hidden;
	text-overflow:ellipsis;
	white-space: nowrap;
}
.items-list{

}
li.item div{
  box-sizing: border-box;
  float: left;
  display: inline-block;
  line-height: 30px;
  height: 30px;
  text-align: left;
  font-size: 13px;
  color: rgb(102,102,102);
  text-indent: 12px;
  white-space: nowrap;
  text-overflow: ellipsis;
  overflow: hidden;
}

li.item:nth-child(odd){
  background-color: rgb(245,245,247);
}

li.item:hover{
  background-color: rgb(236,237,238);
}
</style>
