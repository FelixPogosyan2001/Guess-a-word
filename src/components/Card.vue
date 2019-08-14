<template>
  <div :class="[status ? status : '']" class="col-sm-3 card">
    <slot></slot>
  </div>
</template>
<script>
export default {
  props: ["answer", "status"],
  mounted:function() {
    const recognizer = new webkitSpeechRecognition();
    recognizer.interimResults = true;
    recognizer.lang = "en-En";
    recognizer.onresult = event => {
      var result = event.results[event.resultIndex];
      if (result.isFinal) {
        this.answer(result[0].transcript.toLowerCase());
      }
    };
    recognizer.start();
  }
};
</script>
<style scoped>
.card {
  height: 20vh;
  background: #c44dff;
  display: grid;
  margin: 0 auto;
  animation: appearance 0.5s linear;
}
.card p {
  font-size: 2em;
  align-self: center;
  text-align: center;
  color: white;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
  font-weight: bold;
}
.success {
  background: lightgreen !important;
}
.error {
  background: red !important;
}
@keyframes appearance {
  from {
    transform: scale(0);
  }
  to {
    transform: scale(1);
  }
}
</style>
