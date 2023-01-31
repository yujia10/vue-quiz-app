<script setup>
  import {RouterLink} from "vue-router"
  const {quizQuestionLength, numberOfCorrectAnswers} = defineProps(["quizQuestionLength", "numberOfCorrectAnswers"])
</script>

<template>
  <div class="results">
    <p>Your Results...</p>
    <h1>
      {{numberOfCorrectAnswers}} / {{quizQuestionLength}}
    </h1>
    <RouterLink to="/" class="back">Go Back</RouterLink>
  </div>
</template>

<style scoped>
  .results {
    text-align: center;
    padding: 100px 0;
  }

  p{
    font-size: 25px;
  }

  h1{
    font-size: 80px;
  }

  .back{
    background-color: bisque;
    padding:10px 15px;
    text-decoration: none;
    color:black;
    border-radius: 5px;
  }
  .back:hover {
    background-color:antiquewhite;
  }
</style>
