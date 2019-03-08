<template>
  <div class="lyric">
    <div class="box bg-blur" :style="`background-image:url(${musicimg})`">
      
    </div>
     <div class="disc"></div>
     <div class="mmPlayer-mask"></div>
  </div>
    
</template> 
<script>
import Vue from 'vue' 
export default{
  data () {
    return {
      musicablum:"",
      musicimg:"",
      ablum:"",
      singger:""
    }
  },
  beforeRouteEnter (to, from, next) {
    Vue.http.get(`/newapi/lyric?id=${to.params.id}`).then(response => {
      next(vm => {
        if (!response) {
          vm.$router.push({path: '/'})
        }else{
          Vue.http.get(`/newapi/song/detail?ids=${to.params.id}`).then(response => {
           /*先获取歌手id再获得专辑id*/
           vm.musicablum=response.body.songs[0].alia[0]?response.body.songs[0].alia[0]:""
           Vue.http.get(`/newapi/album?id=${response.body.songs[0].al.id}`).then(response => {
           vm.musicimg=response.body.album.picUrl?response.body.album.picUrl:response.body.ablum.artist.img1v1Url
           console.log(response)
          })
        })
        }
      })
    })
  },
   beforeRouteUpdate (to, from, next) {
     Vue.http.get(`/newapi/lyric?id=${to.params.id}`).then(response => {
      next(vm => {
        if (!response) {
          vm.$router.push({path: '/'})
        }else{

          Vue.http.get(`/newapi/song/detail?ids=${to.params.id}`).then(response => {
           /*先获取歌手id再获得专辑id*/
           this.musicablum=response.body.songs[0].alia[0]?response.body.songs[0].alia[0]:""
           console.log("跳转后",musicablum)
           Vue.http.get(`/newapi/album?id=${response.body.songs[0].al.id}`).then(response => {
           this.musicimg=response.body.album.picUrl?response.body.album.picUrl:response.body.ablum.artist.img1v1Url
           console.log(response)
          })
        })
        }
      })
    })
  }  
}
</script>
<style scoped>
.lyric{
  position: relative;
}
.box{
  height:250px;
  width: 90%;
  overflow-y: scroll;
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
  filter: blur(12px);
  transform: translate(4%, 6%);
  z-index: -5;
  transform: scale(1.5);
  background-color: #fff;
  opacity:0.7;
}
.bg-blur {
   
}
.disc {
  position: absolute;
  top: 0px;
  left: 0px;
  margin-top: 10%;
  margin-left: 10%;
  width: 300px;
  height: 300px;
  border-radius: 300px;
  transform: rotate(45deg); 
  border: 2px solid #131313;
  box-shadow: 0 0 0 10px #343935;
  opacity: 1;
  background-image: url('../../assets/cd.gif');
}
div.head{
  padding:20px 20px 60px 30px;
  width: 100%;
  height: auto;
}

.cover-image{
  width: 200px;
  height: 200px;
  vertical-align: top;
}

.head-right{
  display: inline-block;
  width: calc(100% - 220px);
  padding-left: 30px;
}

.title{
  height: auto;
  overflow: hidden;
}

.title span{
  display: inline-block;
  float: left;
}

.tag{
  font-size: 14px;
  background-color: rgb(198, 47, 47);
  color: white;
  padding: 2px 8px;
  border-radius: 4px;
  font-weight: normal;
}

.name{
  font-size: 20px;
  line-height: 1.0;
  margin-left: 10px;
  font-weight: bold;
  width: 330px;
}

span.play-count,
span.track-count{
  float: right;
  font-size: 12px;
  font-weight: normal;
  height: 20px;
  line-height: 20px;
  width: 40px;
  text-align: right; 
  margin-left: 5px;
  position: relative;
  text-align: left;
  text-indent: 5px;
}

span.play-count::before,
span.track-count::before{
  position: absolute;
  width: 15px;
  height: 15px;
  content: " ";
  top: 2px;
  left: -10px;
  background-size: 15px 15px;
  background-repeat: no-repeat;
}

span.play-count::before{
  background-image: url('../../assets/playcount.png');
}

span.track-count::before{
  background-image: url('../../assets/trackcount.png');
}

.author{
  margin:10px 0px;
  height: 30px;
  line-height: 30px;
}

.author img{
  width: 30px;
  height: 30px;
  border-radius: 30px;
  vertical-align: top;
}

.nickname{
  margin-left: 10px;
  color: rgb(102, 102, 102);
}

.create-time{
  color: rgb(136, 136, 136);
  font-size: 11px;
  margin-left: 20px;
}

.control{
  overflow: hidden;

}

.control  > div{
  float: left;
  border: 1px solid rgb(225,225,226);
  margin-right: 10px;
  padding: 2px 10px;
  padding-left: 25px;
  font-size: 14px;
  border-radius: 5px;
  position: relative;
  cursor: pointer;
}

.control > div:hover{
  background-color: rgb(245, 245, 247);
}

.control > div::before{
  content: ' ';
  position: absolute;
  left: 5px;
  top: 5px;
  width: 15px;
  height: 15px;
  background-size: 15px 15px;
  background-repeat: no-repeat;
}

.add{
  border-left: 1px solid rgb(225,225,226);
  margin-left: 5px;
  text-align: center;
  font-size: 15px;
  padding-left: 5px;
}

.play-all::before{
  background-image: url('../../assets/play2.png');
}

.saved::before{
  background-image: url('../../assets/collect.png');
}

.share-count::before{
  background-image: url('../../assets/share.png');
}

.download-all::before{
  background-image: url('../../assets/download.png');
}

.play-all div {
  float: left;
}

.tags{
  font-size: 13px;
  margin-top: 20px;
  margin-bottom: 10px;
}

.tags span{
  color: rgb(12, 115, 194);
}

.description p{
  overflow : hidden;
  width: 340px;
  font-size: 13px;
  text-overflow: ellipsis;
  line-height: 20px;
  height: 40px;
}

.spread{
  height: auto !important;
}

.drop-down{
  float: right;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
}

.content dl{
  overflow: hidden;
  padding:0px 30px;
  border-bottom: 1px solid rgb(198, 47, 47);
}

dd:not(.search){
  float: left;
  padding: 0px 15px;
  border: 1px solid rgb(225,225,226);
  border-bottom: none;
  margin-right: 10px;
  font-size: 13px;
  height: 30px;
  line-height: 30px;
  cursor: pointer;
}

dd:not(.search):not(.choosed):hover{
  background-color: rgb(245, 245, 247);
}

.choosed{
  background-color: rgb(198, 47, 47); 
  color: white;
}

.search{
  float: right;
}

.search input,
.search input:focus{
  border: 1px solid rgb(225,225,226);
  border-radius: 20px;
  outline-style: none;
  text-indent: 10px;
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
.mmPlayer-mask {
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    z-index: -1;
    background-color: rgba(0,0,0,.4);
    height: 570px;
    width: 100%;
}
</style>
