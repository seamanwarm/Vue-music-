<template>
	<div id="footers" name="footers">
    <div class="songsdetail">
      <div class="music-img">
        <router-link :to="'/lyric/'+this.list[this.currentSong].id" > <img :src="musicimg" alt=""></router-link>
      </div>
      <div class="musicname">
        <p>{{this.list[this.currentSong].name}} <span class='grey'>{{musicablum?musicablum:""}}</span></p>
        <p class="singername grey ">{{this.list[this.currentSong].singer}}</p>
      </div>
    </div>
    <div class="control">
      <img class="pre" src="../assets/music_pre.png" @click="$store.commit('changeSong', 'pre')">
      <img class="play" @click="playMusic" src="../assets/music_play.png" :style="{display: !play ? 'inline-block' : 'none'}">
      <img class="play" @click="pauseMusic" src="../assets/music_stop.png" :style="{display: !play ? 'none' : 'inline-block'}">
      <img class="next" src="../assets/music_next.png" @click="$store.commit('changeSong', 'next')">
    </div>
    <div class="progress">
      <span>{{current}}</span>
      <vue-slider class="playprogress" ref="slider" v-bind="setting" style="display:inline-block;padding:15px 10px;" v-model="progress"></vue-slider>
      <span>{{end}}</span>
      <img class="volume" src="../assets/volume.png">
      <vue-slider class="volumeprogress" ref="slider2" v-bind="setting2" style="display:inline-block;padding:15px 10px;" v-model="volume"></vue-slider>
      <audio 
        @canplay="audioInit" ref="player" 
        @ended="ended" 
        @error="errorLoad"
        style="display:none" :src="mp3Url"  controls="controls"></audio>
    </div>
    <div class="play-way">顺序</div>
    <div class="playlist" tabindex="10" @click.capture="listShow = true" @focus="listShow = true" @blur="listShow = false">{{list.length}}
      <play-list class="list" @set-show="setShow" :list="list" v-show="listShow" :current="currentSong"/>
    </div>
	</div>
</template>
<script >
import VueSlider from 'vue-slider-component'
import PlayList from './play-list'
import storejs from '../store/search.js'
import Vue from 'vue'

export default {
  name: 'footers',
  components: {
    VueSlider,
    PlayList
  },
 
  data () {
    return {
      app: '网易云音乐',
      musicimg:"",
      musicablum:"",

      setting: {
        width: 430,
        tooltip: false,
        dotSize: 13,
        processStyle: {
          'background-color': 'rgb(232,60,60)'
        },
        min: 0,
        max: 200,
        clickable: true,
        speed: 1.0
      },
      progress: 0,
      setting2: {
        width: 100,
        tooltip: 'hover',
        dotSize: 10,
        clickable: true,
        processStyle: {
          'background-color': 'rgb(232,60,60)'
        },
        max: 100,
        min: 0
      },
      volume: 100,
      play: false,
      current: '00:00',
      end: '00:00',
      update: '',
      drag: false,
      listShow: false
    }
   
  },
  mounted: function () {
  },
  methods: {
    audioInit: function () {
      const duration = this.$refs.player.duration
      this.end = Vue.options.filters.timeToStr(duration)
      this.setting.max = Number.parseInt(duration, 10)
      this.playMusic()
    },
    getCurrent: function () {
      const currentTime = this.$refs.player.currentTime
      this.current = Vue.options.filters.timeToStr(currentTime)
      this.progress = Number.parseInt(currentTime, 10)
    },
    playMusic: function () {
      if (!this.mp3Url) {
        return
      }
      this.update = setInterval(this.getCurrent, 1000 / 60)
      this.$refs.player.play()
      this.play = true
    },
    pauseMusic: function () {
      clearInterval(this.update)
      this.$refs.player.pause()
      this.play = false
    },
    ended: function () {
      this.progress = 0
      if (this.current) {
        this.$store.commit('changeSong', "next")
      }
    },
    errorLoad: function () {
      if (this.mp3Url === 'error') {
        return
      }
      alert('该歌曲网易云具有版权，无法播放')
      this.play = false
    },
    setShow: function (show) {
      this.listShow = show
    }
  },
  computed: {
    mp3Url: function () {
      let list = this.$store.state.search.songList
      if (list.length === 0) {
        this.ended()
        return 'error'
      }
       Vue.http.get(`/newapi/song/detail?ids=${list[this.currentSong].id}`).then(response => {
           
           /*先获取歌手id再获得专辑id*/
           this.musicablum=response.body.songs[0].alia[0]?response.body.songs[0].alia[0]:""
           
           Vue.http.get(`/newapi/album?id=${response.body.songs[0].al.id}`).then(response => {
           
            this.musicimg=response.body.album.picUrl?response.body.album.picUrl:response.body.ablum.artist.img1v1Url

          })
        })
      if (list[this.currentSong].mp3Url === null) {
        Vue.http.get(`/newapi/music/url?id=${list[this.currentSong].id}`).then(response => {
          list[this.currentSong].mp3Url = response.body.data[0].url
          this.$store.commit('updateSongList', list)
        })
      }
      console.log(list[this.currentSong])
      return list[this.currentSong].mp3Url
    },
    list: function () {
      return this.$store.state.search.songList
    },
    currentSong: function () {
      return this.$store.state.search.currentSong
    }
  },
  watch: {
    progress: function (newValue, oldValue) {
      
      if (Math.abs(newValue - oldValue) > 1) {
        this.current = Vue.options.filters.timeToStr(newValue)
        this.$refs.player.currentTime = newValue
      }
    },
    volume: function (newValue) {
      this.$refs.player.volume = newValue / 100
    }
  }
}

</script>
<style scoped>
*{
  box-sizing: border-box;
}

#footers{
	height: 50px;
	width: 100%;
  background-color: rgb(246,246,248);
  border: 1px solid rgb(225,225,226);
  padding: 5px 0px;
  padding-left: 30px;
  position: relative;
}

.pre,
.next{
  width: 30px;
  height: 30px;
  cursor: pointer;
  border-radius: 30px;
  position: relative;
  top: -5px;
}

.play{
  width: 40px;
  height: 40px;
  border: 40px;
  cursor: pointer;
  margin: 0 15px;
}

.control,
.progress{
  display: inline-block;
  float: left;
  height: 100%;
  line-height: 50px;
  margin-left: 20px;
}

.progress span{
  position: relative;
  top: -10px;
}

.volume{
  width: 20px;
  height: 20px;
  opacity: 0.5;
  position: relative;
  top:-8px;
  left: 5px;
}

.playlist{
  position: absolute;
  right: 20px;
  width: 45px;
  height: 20px;
  padding-right: 4px;
  text-align: right;
  background-image: url('../assets/playlist.jpg');
  background-position: 0px 0px;
  background-size: 20px 25px;
  background-repeat: no-repeat;
  margin-top: 10px;
  font-size: 12px;
  line-height: 20px;
  background-color: rgb(225,225,226);
  border-bottom-right-radius: 10px;
  border-top-right-radius: 10px;
  cursor: pointer;
  outline: none;
}

.list{
  position: absolute;
  width: 580px;
  height: 480px;
  right: -20px;
  top:-495px;
  z-index: 100;
  cursor: default;
}
</style>
<style>
 .vue-slider-dot{
  background: url('../assets/point.png') no-repeat;
  box-shadow: none;
  border-radius: 0;
  position: relative;
}

.playprogress .vue-slider-dot{
  background-size: 5px 5px;
  background-position: 4px;
}

.volumeprogress .vue-slider-dot{
  background-size: 4px 4px;
  background-position: 3px;
}
.songsdetail{
  position: absolute;
  width: 204px;
  height: 63px;
  border: 1px solid #e1e1e2;
  top: -64px;
  left: -1px;
  background-color: #f6f6f8;
  border-bottom: none;
}
.songsdetail div{
  float: left;
  height: 63px;
  font-size: 12px;
  color: #333333;
  margin:3px;
  overflow:hidden;  

}
.music-img{
  width: 50px;
  height: 63px;
}
.music-img img{
  width: 50px;
  height: 50px;
  margin:3px; 
  cursor: pointer;
}
.musicname{
  margin-top: 10px !important;
}
.musicname p{
  height: 22px;
  line-height: 28px;
  width: 140px;
  overflow:hidden;
  text-overflow: ellipsis;
  white-space: nowrap; 
}
.musicname span{
  display: inline-block;
  width: 75px;
  height: 20px;
 
  overflow:hidden;
  text-overflow: ellipsis;
  white-space: nowrap; 
}
.singername{
  padding: 3px;
}
.grey{
  color: #666;
}
.play-way{
  position: absolute;
  right: 65px;
  width: 45px;
  height: 20px;
  padding-right: 4px;
  text-align: right;
  background-image: url('../assets/playlist.jpg');
  background-position: 0px 0px;
  background-size: 20px 25px;
  background-repeat: no-repeat;
  margin-top: 10px;
  font-size: 12px;
  line-height: 20px;
  background-color: rgb(225,225,226);
  border-bottom-right-radius: 10px;
  border-top-right-radius: 10px;
  cursor: pointer;
  outline: none;
}
</style>
