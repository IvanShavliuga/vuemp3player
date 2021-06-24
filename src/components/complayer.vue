<template>
  <div class="playlist__player">
    <audio
      controls
      class="audio">
      <source
        :src="file"
        type="audio/mpeg">
      Тег audio не поддерживается вашим браузером.
      <a :href="file">Скачайте музыку</a>.
    </audio>
    <span class="playlist__debug">{{ shortName }}</span>
  </div>
</template>
<script>
export default {
  props: {
    file: {
      type: String,
      default: 'none'
    }
  },
  computed: {
    shortName () {
      return this.file.substring(this.file.length - 17)
    }
  }
}
</script>
