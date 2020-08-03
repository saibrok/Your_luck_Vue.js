<template>
  <div class="progress">
    <div class="progress-bar" v-bind:style="width"></div>
  </div>
</template>

<script>
export default {
  props: {
    max: Number,
    val: Number,
  },
  computed: {
    width() {
      let width = (this.val / this.max) * 100;

      if (width > 100) {
        width = 100;
      }

      if (width < 0) {
        width = 0;
      }

      return {
        width: `${width}%`,
      };
    },
  },
};
</script>