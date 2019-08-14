<template>
  <div class="col-3 progress">
    <div
      ref="progress"
      class="progress-bar progress-bar-striped progress-bar-animated"
      role="progressbar"
      aria-valuenow="75"
      aria-valuemin="0"
      aria-valuemax="100"
      :style="{width:width + '%'}"
    ></div>
  </div>
</template>
<script>
export default {
  props: ["word", "next", "speech"],
  data: () => {
    return {
      width: 100,
      time: 0
    };
  },
  mounted: function() {
    if (this.word <= 6 && this.word > 4) var letter = 0.85;
    else if (this.word <= 4 ) var letter = 1.1;
    else var letter = 0.6; 
    this.time = this.word * letter;
    this.$refs.progress.style.animation = `bar ${this.time}s linear`;
    setTimeout(() => {
      if (!this.speech) this.next();
      else return false;
    }, this.time * 1000);
  },
  watch: {
    speech(value) {
      this.speech = value;
    }
  }
};
</script>
<style>
.progress {
  margin: 40px auto;
  padding: 0px;
}
@keyframes bar {
  from {
    width: 100%;
  }
  to {
    width: 0%;
  }
}
</style>
