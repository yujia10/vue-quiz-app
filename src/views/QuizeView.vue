<script setup>
import Question from "../components/Question.vue";
import {useRoute} from "vue-router";
import {ref, watch, computed} from "vue";
import quizes from "../data/quizes.json"

const route = useRoute()

const quizId = parseInt(route.params.id)

const quiz = quizes.find(q=>q.id === quizId)

const currentQuestionIndex =ref(0);

const numberOfCorrectAnswers = ref(0)

// const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)

// watch(() => currentQuestionIndex.value, ()=>{
//   questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
// })

const questionStatus = computed(()=>{
  return `${currentQuestionIndex.value}/${quiz.questions.length}`
})

const barPercentage = computed(()=>{
  return `${currentQuestionIndex.value/quiz.questions.length * 100}%`
})

const onOptionSeleted =(isCorrect) => {
  if(isCorrect){
    numberOfCorrectAnswers++;
  }

  currentQuestionIndex.value++
}

</script>

<template>
  <div>
   <header>
    <h4>Question {{ questionStatus }}</h4>
    <div class="bar">
      <div class="completion" :style="{width: barPercentage}"></div>
    </div>
   </header>
    <div>
      <Question
        :question="quiz.questions[currentQuestionIndex]"
        @selectOption="onOptionSeleted"/>
    </div>

    <button @click="currentQuestionIndex++">Next Question</button>
  </div>
</template>

<style scoped>
  header{
    margin-top: 20px;
  }

  header h4 {
    font-size: 30px;
    margin-bottom: 5px;
  }

  .bar {
    width: 300px;
    height: 50px;
    border: 3px solid bisque;
  }

  .completion{
    height: 100%;
    width: 0%;
    background-color: bisque;
  }


</style>
