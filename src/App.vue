<template>
  <div id="app">
    <header>JS30 Day1 Drum Kit</header>
    <div class="keys">
      <div
        class="button"
        v-for="key in keyList"
        :key="key.keyCode"
        :class="[key.isPlaying ? 'playing' : '']"
        @transitionend="removeTransition($event, key)"
      >
        <div class="button_keyName">{{ key.keyName }}</div>
        <div class="button_sound">{{ key.sound }}</div>
      </div>
    </div>
    <footer>Chaco Wang</footer>
  </div>
</template>

<script>
import clap from "../src/assets/sounds/clap.wav";
import hihat from "../src/assets/sounds/hihat.wav";
import kick from "../src/assets/sounds/kick.wav";
import boom from "../src/assets/sounds/boom.wav";
import openhat from "../src/assets/sounds/openhat.wav";
import ride from "../src/assets/sounds/ride.wav";
import snare from "../src/assets/sounds/snare.wav";
import tom from "../src/assets/sounds/tom.wav";
import tink from "../src/assets/sounds/tink.wav";
export default {
  name: "App",
  data() {
    return {
      keyList: [
        {
          keyName: "A",
          sound: "CLAP",
          keyCode: 65,
          soundSrc: clap,
          isPlaying: false,
        },
        {
          keyName: "S",
          sound: "HIHAT",
          keyCode: 83,
          soundSrc: hihat,
          isPlaying: false,
        },
        {
          keyName: "D",
          sound: "KICK",
          keyCode: 68,
          soundSrc: kick,
          isPlaying: false,
        },
        {
          keyName: "F",
          sound: "OPENHAT",
          keyCode: 70,
          soundSrc: openhat,
          isPlaying: false,
        },
        {
          keyName: "G",
          sound: "BOOM",
          keyCode: 71,
          soundSrc: boom,
          isPlaying: false,
        },
        {
          keyName: "H",
          sound: "RIDE",
          keyCode: 72,
          soundSrc: ride,
          isPlaying: false,
        },
        {
          keyName: "J",
          sound: "SNARE",
          keyCode: 74,
          soundSrc: snare,
          isPlaying: false,
        },
        {
          keyName: "K",
          sound: "TOM",
          keyCode: 75,
          soundSrc: tom,
          isPlaying: false,
        },
        {
          keyName: "L",
          sound: "TINK",
          keyCode: 76,
          soundSrc: tink,
          isPlaying: false,
        },
      ],
    };
  },
  methods: {
    playSound(e) {
      const key = this.keyList.find((key) => key.keyCode === e.keyCode);
      if (!key) {
        return;
      }
      key.isPlaying = true;
      const audio = new Audio(key.soundSrc);
      audio.currentTime = 0;
      audio.play();

      //音訊播放結束時移除class
      audio.onended = function () {
        key.isPlaying = false;
      };
    },
    removeTransition(e, key) {
      if (e.propertyName !== "transform") return;
      key.isPlaying = false;
    },
  },
  created() {
    window.addEventListener("keydown", this.playSound);
  },
};
</script>

<style>
body,
html {
  margin: 0;
  padding: 0;
  font-family: sans-serif;
}
html {
  font-size: 10px;
  background: url("./assets/background.jpg") bottom center,
    linear-gradient(#ffc600, 10%, #193549);
  background-size: cover;
}
#app {
  width: 100vw;
  height: 100vh;
}

header {
  width: 100%;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3.5rem;
  font-family: "Square Peg", cursive;
  letter-spacing: 1rem;
  background-color: rgba(200, 200, 200, 0.8);
}

footer {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 2rem;
  position: fixed;
  bottom: 0;
  font-size: 1rem;
  font-weight: 200;
  letter-spacing: 2px;
  color: #fff;
  background-color: rgba(46, 43, 43, 0.7);
}
.keys {
  width: 100%;
  height: calc(100% - 100px - 2rem);
  display: flex;
  flex: 1;
  align-items: center;
  justify-content: center;
}
.button {
  border: 0.4rem solid black;
  border-radius: 0.5rem;
  margin: 1rem;
  font-size: 1.5rem;
  padding: 1rem 0.5rem;
  transition: all 0.07s ease;
  width: 10rem;
  text-align: center;
  color: white;
  background: rgba(0, 0, 0, 0.4);
  text-shadow: 0 0 0.5rem black;
}
.button_keyName {
  display: block;
  font-size: 4rem;
}
.button_sound {
  font-size: 1.2rem;
  text-transform: uppercase;
  letter-spacing: 0.1rem;
  color: #ffc600;
}
.playing {
  transform: scale(1.1);
  border-color: #ffc600;
  box-shadow: 0 0 1rem #ffc600;
}
</style>
