<template>
<div class="container">
    <h1>Hello {{ student }}</h1>
    <button @click="changeStudents">Change Students</button>
</div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home",
  components: {},
  data() {
    return{
       student: "Harry",
    };
  },
  methods: {
    changeStudents: function() {
      this.student = "Charlene";
    },
  },
};

</script>



<style lang="scss" scoped>
  h1 {
  font-size: 3rem;  
  }
</style>
