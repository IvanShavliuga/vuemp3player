<template>
  <span>
    <span class="playlist__prev" @click="prev">prev</span>
    <span class="playlist__counter">
      page {{ pagecurr }} of {{ maxvalue }}
    </span>
    <span class="playlist__next" @click="next">next</span>
    <br />
  </span>
</template>
<script>
export default {
  props: {
    pagecurr: {
      type: Number,
      default: 0,
    },
    maxvalue: {
      type: Number,
      default: 5,
    },
  },
  methods: {
    next() {
      if (this.pagecurr < this.maxvalue) {
        this.$emit("update", this.pagecurr + 1);
      }
    },
    prev() {
      if (this.pagecurr > 1) {
        this.$emit("update", this.pagecurr - 1);
      }
    },
  },
};
</script>
