<template>
  <div class="playlist__player">
    <audio controls :class="noStandard ? 'nostandard' : 'audio'">
      <source :src="file" type="audio/mpeg" />
      Тег audio не поддерживается вашим браузером.
      <a :href="file">Скачайте музыку</a>.
    </audio>
    <div v-if="noStandard">
      <slot name="playerControl" @play="playClick" @pause="pauseClick"> </slot>
    </div>
    <span class="playlist__debug">{{ shortName }} {{ timeStamp }}</span>
    <div v-if="noStandard">
      <slot name="playerList"> </slot>
    </div>
    <div v-if="noStandard">
      <slot name="playerPages"> </slot>
    </div>
  </div>
</template>
<script>
export default {
  name: "ivplayer",
  props: {
    file: {
      type: String,
      default: "none",
    },
    noStandard: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      audioTag: null,
      buttons: null,
      volume: null,
      metaData: null,
      timeStamp: 0,
    };
  },
  computed: {
    shortName() {
      return this.file.substring(this.file.length - 17);
    },
  },
  methods: {
    playClick() {
      this.audioTag.play();
    },
    pauseClick() {
      this.audioTag.pause();
    },
    prevClick() {
      console.log("prev");
    },
    nextClick() {
      console.log("next");
    },
    stopClick() {
      this.audioTag.pause();
    },
  },
  mounted() {
    this.audioTag = document.querySelector("audio");
    const btnPlay = document.querySelector("#playControl");
    const btnPause = document.querySelector("#pauseControl");
    const btnPrev = document.querySelector("#prevControl");
    const btnNext = document.querySelector("#nextControl");
    this.buttons = [btnPlay, btnPause, btnPrev, btnNext];
    this.volume = this.audioTag.volume;
    this.audioTag.addEventListener("progress", (el) => {
      console.log(el);
      console.log(this.audioTag.buffered);
    });
    this.audioTag.addEventListener("timeupdate", (el) => {
      this.timeStamp = el.timeStamp;
    });
    console.log(this.audioTag.buffered);
    this.audioTag.addEventListener("ended", ({ ...arg }) => console.log(arg));
    if (btnPause) {
      btnPlay.addEventListener("click", () => this.playClick());
    }
    if (btnPlay) {
      btnPause.addEventListener("click", () => this.pauseClick());
    }
    if (btnPrev) {
      btnPrev.addEventListener("click", () => this.prevClick());
    }
    if (btnNext) {
      btnNext.addEventListener("click", () => this.nextClick());
    }
  },
};
</script>
<style scoped>
.nostandard {
  display: none;
}
</style>
