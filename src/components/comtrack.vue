<template>
  <div
    :class="['playlist__item', selectid === index ? 'itemactive' : '']"
    @click="selectfile(index)"
  >
    <div class="playlist__number">#{{ getID(index) }}</div>
    <div class="playlist__name">
      <span>Track: </span>
      <span>{{ getID(index) }}</span>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    selectid: {
      type: Number,
      default: 0,
    },
    index: {
      type: Number,
      default: 0,
    },
    pagecurr: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    getID(x) {
      return (this.pagecurr - 1) * 10 + x;
    },
    selectfile(id) {
      this.$emit("select", id - 1);
    },
  },
};
</script>
