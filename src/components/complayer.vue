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
    <span class="playlist__debug">{{ shortName }} {{ volume }}</span>
  </div>
</template>
<script>
export default {
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
    stopClick() {
      this.audioTag.pause();
    },
  },
  mounted() {
    this.audioTag = document.querySelector("audio");
    const btnPlay = document.querySelector("#playControl");
    const btnPause = document.querySelector("#pauseControl");
    const btnStop = document.querySelector("#stopControl");
    this.volume = this.audioTag.volume;
    this.audioTag.addEventListener("progress", ({ ...arg }) =>
      console.log(arg)
    );
    if (btnPause && btnPlay && btnStop) {
      btnPlay.addEventListener("click", () => this.playClick());
      btnPause.addEventListener("click", () => this.pauseClick());
      btnStop.addEventListener("click", () => this.stopClick());
      this.buttons = [btnPlay, btnPause, btnStop];
      console.log(this.buttons);
    }
  },
};
</script>
<style scoped>
.nostandard {
  display: none;
}
</style>
