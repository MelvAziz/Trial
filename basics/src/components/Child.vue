<template>
  <div>
    <h1></h1>
    <ul class="Quiz-Questions">
      <li class="Quiz-item">{{ flavor }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Child",
  data() {
    return { 
      question: {},
      choices: [],
    };
  },
  mounted: function() {
    this.fetchData();
  },
  methods: {
    fetchData: async function() {
      try {
        const result = await fetch (`https://opentdb.com/api.php?amount=10&category=23&difficulty=medium&type=multiple`);
        const data = await result.json();
        console.log(data);
        this.question = data.results.question;
        this.choices = [data.results.correct_answer, data.results.incorrect_answer[0], data.results.incorrect_answer[1], data.results.incorrect_answer[2]];
      }
      catch(error) {
        alert(error);
      }
    },
  },
};
</script>

<style></style>