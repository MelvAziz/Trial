<template>
  <div class="container">
    <h1>Welcome to this Quiz Game!</h1>
    <h1 v-if="started"> {{ Question[QuestionN] }}</h1>
    <button v-if="started === true && clickable === true" v-on:click="checkAnswer"> {{ Choice1[QuestionN] }} </button>
    <button v-else-if="started === true"> {{ Choice1[QuestionN] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ Choice2[QuestionN] }} </button>
    <button v-else-if="started === true"> {{ Choice2[QuestionN] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ Choice3[QuestionN] }} </button>
    <button v-else-if="started === true"> {{ Choice3[QuestionN] }} </button>
    <button v-if="started && clickable === true" v-on:click="checkAnswer"> {{ Choice4[QuestionN] }} </button>
    <button v-else-if="started === true"> {{ Choice4[QuestionN] }} </button>
    <button v-on:click="startedQuiz" v-else>Begin</button>
    <button v-on:click="nextQuestion" v-if="submit">Submit</button>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home",
  components: {},
  data() {
    return {
      Question: ["Who is the first president of the United States?", "How many years old is Melvin Aziz?"],
      Choice1: ["Thomas Jefferson", "10"],
      Choice2: ["James Madison", "13"],
      Choice3: ["George Washington", "14"],
      Choice4: ["Abraham Lincoln", "16"],
      correctAnswer: [1,3,0,2,0,2,3,1,2,0],
      QuestionN: 0,
      started: false,
      submit: false,
      clickable: false,
    };
  },
  methods: {
    startedQuiz: function() {
      this.started = true;
      this.clickable = true;
    },
    checkAnswer: function() {
      this.submit = true;
      this.clickable = false;
    },
    nextQuestion: function () {
      this.submit = false;
      this.clickable = true;
      this.QuestionN ++;
    }

  },
  created() {},
  mounted() {  },
  beforeCreate() {},
};
</script>

<style lang="scss" scoped>
h1 {
  font-size: 3rem;
}
button {
  font-size: 2rem;
}
</style>