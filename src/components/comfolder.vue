<template>
  <span>
    <span
      class="playlist__prev"
      @click="prev">prev</span>
    <span class="playlist__counter"> folder {{ folder }} of 2 </span>
    <span
      class="playlist__next"
      @click="next">next</span>
  </span>
</template>
<script>
export default {
  props: {
    folder: {
      type: Number,
      default: 0
    },
    maxvalue: {
      type: Number,
      default: 5
    }
  },
  methods: {
    next () {
      if (this.folder < this.maxvalue) {
        this.$emit('update', this.folder + 1)
      }
    },
    prev () {
      if (this.folder > 1) {
        this.$emit('update', this.folder - 1)
      }
    }
  }
}
</script>
