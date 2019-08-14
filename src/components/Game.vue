<template>
  <div class="game">
    <h3 v-if="!active" class="game__title">Game wil start in {{time}}</h3>
    <Score v-else-if="active == 'end'" :user="user" :allWords="countOfWords" :count="count" />
    <div v-else-if="active == 'start'">
      <Card :answer="check" :status="status" :key="key">
        <p>{{word | upper}}</p>
      </Card>
      <center>
        <i class="microphone fas fa-microphone-alt"></i>
      </center>
      <Indicator :speech="speech" :next="autoChange" :key="mod" :word="word.length" />
    </div>
  </div>
</template>
<script>
import Card from "./Card.vue";
import Indicator from "./Indicator.vue";
import Score from "./Score.vue";

const getWords = level => require("../database/words.js")[level];

function reversing(word) {
  if (!word) return false;
  return word
    .split("")
    .reverse()
    .join("");
}

function isEnd(length) {
  if (length == 0) {
    this.active = "end";
  }
}

function randomWords(arr) {
  var new_words = [];
  var length = arr.length;

  for (var i = 0; i < length; i++) {
    let index = change(arr.length);
    new_words.push(arr[index]);
    arr.splice(index, 1);
  }

  return new_words;
}

function change(n) {
  return Math.floor(Math.random() * n);
}

function newSettings(timer) {
  setTimeout(() => {
    this.status = null;
    this.key = Math.random();
    this.mod = Math.random();
    this.data.shift();
    this.speech = false;
    isEnd.call(this, this.data.length);
    this.word = reversing(this.data[0]);
  }, timer);
}

const option = {
  props: ["user", "choice", "countOfWords"],
  data: function() {
    return {
      time: 3,
      active: false,
      data: null,
      word: null,
      count: 0,
      status: null,
      key: Math.random(),
      mod: Math.random(),
      speech: false
    };
  },
  components: {
    Card,
    Indicator,
    Score
  },
  beforeMount: function() {
    const timer = () => {
      setInterval(() => {
        if (this.time == 0 && !this.active) {
          this.active = "start";
          return false;
        }
        this.time--;
      }, 1000);
    };
    timer();
    this.data = randomWords(getWords(this.choice)).slice(0, this.countOfWords);
    this.word = reversing(this.data[0]);
  },
  methods: {
    check(answer) {
      this.speech = true;
      if (reversing(this.word) == answer) {
        this.count++;
        this.status = "success";
        newSettings.call(this, 300);
      } else if (reversing(this.word) != answer && typeof answer == "string") {
        this.status = "error";
        newSettings.call(this, 300);
      }
    },
    autoChange() {
      newSettings.call(this, 0);
    }
  },
  filters: {
    upper: function(value) {
      return value.toUpperCase();
    }
  }
};
export default option;
</script>
<style>
.microphone {
  color: red;
  font-size: 4em;
  margin-top: 20px;
}
.game__title {
  color: white;
  text-align: center;
  margin: 50px;
}
#next {
  margin-top: 40px;
}
</style>