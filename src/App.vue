<template>
  <div class = 'content'>
    <h1 class = 'content__title'>Guess a word</h1>
    <Game :user = 'user' :choice = "choice" :countOfWords = "countOfWords" v-if = "start" />
    <Sample :begin = "begin" v-else/>
  </div>
</template>

<script>
import Sample from './components/Sample.vue';
import Game from './components/Game.vue';

export default {
  name: 'app',
  components: {
   Sample,
   Game
  },
  data () {
    return {
      start : false,
      user : '',
      choice : '',
      countOfWords : 0
    }
  },
  methods : {
    begin(name,level,words) {
      this.user = name;
      this.choice = level;
      this.countOfWords = words;
      this.start = true
    }
  }
}

</script>

<style scope>
.content__title {
  color:rgb(179, 255, 93);
  text-shadow : 1px 1px 8px rgb(179, 255, 93);
  text-align:center;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin:5vh;
}
</style>
