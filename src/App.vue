<template >
  <section class="mainSec">
    <header class="head">
      <h1>Ocama's Music App</h1>
    </header>
    <section class="player">
      <h2 class="song-title">
        <marquee direction="loop" height="30" width="130" bgcolor="white"
          >{{ current.title }} - {{ current.artist }}</marquee
        >
      </h2>
      <div class="controls">
        <button class="prev" @click="prev()">
          <i class="fas fa-backward"></i>
        </button>
        <button class="pause" v-if="isPlaying" @click="pause()">
          <i class="fas fa-pause"></i>
        </button>
        <button class="play" v-else @click="play()">
          <i class="fas fa-play"></i>
        </button>
        <button class="next" @click="prev()">
          <i class="fas fa-forward"></i>
        </button>
      </div>
    </section>
    <section class="playlist">
      <h3>PLAYLIST</h3>
      <button
        class="song"
        v-for="list in musiclist"
        :key="list.src"
        @click="play(list)"
        :class="list.src == current.src ? 'song playing' : 'song'"
      >
        {{ list.title }} - {{ list.artist }}
      </button>
    </section>
  </section>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      musiclist: [
        {
          artist: "Gryffin",
          title: "Cry",
          src: require("./assets/music/Cry.mp3"),
        },
        {
          artist: "Warriyo",
          title: "Mortals",
          src: require("./assets/music/Mortals.mp3"),
        },
        {
          artist: "HallMan",
          title: "Get it Right Now",
          src: require("./assets/music/getitrightnow.mp3"),
        },
        {
          artist: "Alan Walker",
          title: "I'm Sorry",
          src: require("./assets/music/Sorry.mp3"),
        },
        {
          artist: "Travis Scott",
          title: "Goosebumps",
          src: require("./assets/music/goosebumps.mp3"),
        },
        {
          artist: "Reea",
          title: "Rain",
          src: require("./assets/music/rain.mp3"),
        },
        {
          artist: "Ariana",
          title: "Waterfalls",
          src: require("./assets/music/waterfall.mp3"),
        },
        {
          artist: "Sandra N",
          title: "Chameleon",
          src: require("./assets/music/chameleon.mp3"),
        },
        {
          artist: "JVLA",
          title: "Such a Whore",
          src: require("./assets/music/whore.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song != "undefined") {
        this.player.src = song.src;
        this.player.play();
        this.isPlaying = true;
        this.current = song;
      } else {
        this.player.src = this.current.src;
        this.player.play();
        this.isPlaying = true;
      }
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.musiclist.length - 1;
      }
      this.player.src = this.musiclist[this.index].src;
      this.current = this.musiclist[this.index];
      this.player.play();
    },
    next() {
      this.index++;
      if (this.index > this.musiclist.length - 1) {
        this.index = 0;
      }
      this.player.src = this.musiclist[this.index].src;
      this.current = this.musiclist[this.index];
      this.player.play();
    },
  },
  created() {
    this.current = this.musiclist[this.index];
  },
};
</script>

<style>
body,
html {
  background: url("./assets/page-bg.jpg") no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  font-family: arial;
}
.song-title marquee {
  background: transparent;
  color: white;
}
.head {
  width: 100%;
  height: 50px;
  text-align: center;
  align-items: center;
  color: white;
  padding: 35px 0px;
}
.player {
  align-items: center;
  text-align: center;
}
.mainSec {
  width: 35%;
  margin: 30px auto;
  background-color: #000000bd;
}
.song-title {
  color: #53565a;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
}
.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.play,
.pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #e20000;
}
.next,
.prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #000000;
}
.playlist {
  width: 80%;
  margin: auto;
  width: 100%;
  margin: auto;
  background-color: #92929252;
  padding: 0px 0px 23px 0px;
}
.playlist h3 {
  color: #ffffff;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 0px;
  text-align: center;
  background: #980000;
  padding: 20px 3px;
  margin-top: 0px;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
  color: whitesmoke;
}
.playlist .song:hover {
  color: #ff5858;
}
.playlist .song.playing {
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}
</style>
