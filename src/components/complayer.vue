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
    <span class="playlist__debug">{{ file }}</span>
  </div>
</template>
<script>
export default {
  props: {
    file: {
      type: String
    }
  }
}
</script>
