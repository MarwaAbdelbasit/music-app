<template>
  <div class="app">

    <header>
      <h2 class="logo">
        <i class='bx bx-music' style='color:#d95284'  ></i>
        MUSIC
      </h2>
    </header>

    <main>

      <section class="player">
        <div class="song">
          <h2 class="song-title">{{current.title}} ( <span> {{current.artist}}</span> )</h2>
          <img :src="current.img" class="song-img" alt="">
        </div>
        <div class="control">
          <button class="prev" @click="prev">
            <i class='bx bx-skip-previous-circle' style='color:#d95284' ></i>
          </button>
          <button class="play" v-if="!isPlaying" @click="play">
            <i class='bx bx-play-circle' style='color:#d95284'  ></i>
          </button>
          <button class="pause" v-else @click="pause">
            <i class='bx bx-pause-circle' style='color:#d95284' ></i>
          </button>
          <button class="next" @click="next">
            <i class='bx bx-skip-next-circle' style='color:#d95284'  ></i>
          </button>
        </div>
      </section>

      <section class="playlist">
        <h2>
          <i class='bx bxs-playlist' style='color:#f27e63'  ></i>
          the playlist
        </h2>
        <button v-for="song in songs"
        :key="song.src"
        @click="play(song)"
        :class="(song.src == current.src) ? 'song-playing' : 'song'">
        <i class='bx bx-right-arrow' style='color:#d95284' v-if="(song.src == current.src)"></i>
        {{song.title}} - {{song.artist}}
      </button>
      </section>

    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      isPlaying: false,
      current: {},
      index: 0,
      songs: [
        {
          title: 'send my love to your new lover',
          artist: 'Adele',
          src: require('./assets/Adele - Send My Love To Your New Lover.mp3'),
          img: require('@/assets/adele-send-my-love.jpg'),
          // state: false
        },
        {
          title: 'i want it that way',
          artist: 'Backstreet boys',
          src: require('./assets/Backstreet_Boys_I_Want_It_That_Way_Lyrics_.mp3'),
          img:require('@/assets/Backstreet-Boys.jpg'),
          // state: false
        },
        {
          title: 'on my way',
          artist: 'alan walker & farruko',
          src: require('./assets/Alan Walker & Farruko - On My Way (Lyrics) ft. Sabrina Carpenter.mp3'),
          img:require('./assets/onmyway.jpg'),
          // state: false
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play(song) {
      if(typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
      // this.current.state = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    prev() {
      this.index--;
      if(this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    next() {
      this.index++;
      if(this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    //this.player.play();
    console.log(this.current.img);
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Yusei Magic', sans-serif;
}

button {
  outline: none;
}

header {
  font-size: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #eee;
  width: 100%;
}

main {
  display: flex;
  justify-content: space-evenly;
}

.player {
  width: 50%;
}

.song {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.song-title{
  text-align: center;
  color: #0476D9;
  margin: 20px 0 20px 0;
}

.song-title span {
  color: #F27E63;
}

.song-img {
  width: 300px;
  height: 300px;
  border-radius: 50%;
  margin: 20px 0 20px 0;
}

.control {
  display: flex;
  justify-content: center;
}

.control button {
  margin: 20px;
  border: none;
  background: none;
  font-size: 80px;
}

.playlist {
  background-color: #d9d9d9;
  width: 50%;
  padding:20px 40px;
}

.playlist h2 {
  margin-bottom: 15px;
  color: #F27E63;
}

.playlist button {
  border: none;
  background: none;
  font-size: 20px;
}

.playlist .song-playing {
  color: #D95284;
}

.playlist .song {
  color: #0442BF;
}

</style>
