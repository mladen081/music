<template>
  <div class="home-cont bg-brand-dark-blue-1 pt-16">
    <h1 style="margin-top: 35px">Coming Soon</h1>

    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} - <span>{{ current.artist }}</span>
        </h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <h3>The Playlist</h3>
        <button
          v-for="song in songs"
          :key="song.src"
          @click="play(song)"
          :class="song.src == current.src ? 'song playing' : 'song'"
        >
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: "test song 1",
          artist: "test artist 1",
          src: "/s1.mp3",
        },
        {
          title: "test song 2",
          artist: "test artist 2",
          src: "/s2.mp3",
        },
      ],
      player: new Audio(),
    };
  },
  methods: {
    async play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      await this.player.play();
      this.player.addEventListener(
        "ended",
        function () {
          this.index++;
          if (this.index > this.songs.length - 1) {
            this.index = 0;
          }
          this.current = this.songs[this.index];
          this.play(this.current);
        }.bind(this)
      );
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  },
  beforeUnmount() {
    this.player.pause();
    this.isPlaying = false;
  },
};
</script>

<style scoped>
.home-cont {
  background-image: url("@/assets/home_back.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  height: 1100px;
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title {
  color: #fff;
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
  padding: 15px 15px;
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
  font-weight: 700;
  padding: 10px 15px;
  margin: 0px 15px;
  border-radius: 6px;
  width: 150px;
  border: 1px solid #fff;
}
.next,
.prev {
  font-weight: 700;
  padding: 10px 15px;
  margin: 0px 15px;
  border-radius: 6px;
  border: 1px solid #fff;
}
.playlist {
  padding: 0px 20px;
}
.playlist h3 {
  font-weight: 400;
  margin-bottom: 15px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover {
  opacity: 0.8;
}
.playlist .song.playing {
  opacity: 0.8;
}

@media (max-width: 767px) {
  .next,
  .prev {
    margin: 10px 0;
  }

  .home-cont {
    height: 800px;
  }
}
</style>
