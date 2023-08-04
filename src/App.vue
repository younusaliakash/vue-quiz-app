<script setup>
import { reactive, ref } from "vue";
import Questions from "./components/Questions.vue";
import Result from "./components/Result.vue";

const totalAnsweredQuestion = ref(0);
const totalCorrectAnswer = ref(0);

const quizQuestions = reactive([
  {
    q: "What is 2 + 2?",
    answers: [
      {
        text: "4",
        is_correct: true,
      },
      {
        text: "3",
        is_correct: false,
      },
      {
        text: "Fish",
        is_correct: false,
      },
      {
        text: "5",
        is_correct: false,
      },
    ],
  },
  {
    q: 'How many letters are in the word "Banana"?',
    answers: [
      {
        text: "5",
        is_correct: false,
      },
      {
        text: "7",
        is_correct: false,
      },
      {
        text: "6",
        is_correct: true,
      },
      {
        text: "12",
        is_correct: false,
      },
    ],
  },
  {
    q: "Find the missing letter: C_ke",
    answers: [
      {
        text: "e",
        is_correct: false,
      },
      {
        text: "a",
        is_correct: true,
      },
      {
        text: "i",
        is_correct: false,
      },
    ],
  },
]);

const results = reactive([
  {
    min: 0,
    max: 2,
    title: "Try again!",
    desc: "Do a little more studying and you may succeed!",
  },
  {
    min: 3,
    max: 3,
    title: "Wow, you're a genius!",
    desc: "Studying has definitely paid off for you!",
  },
]);

const answered = ( is_correct) => {
  if(is_correct) {
    totalCorrectAnswer.value++
  }
  totalAnsweredQuestion.value++
}

function reset() {
  totalAnsweredQuestion.value = 0;
  totalCorrectAnswer.value = 0;
}
</script>

<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <Questions
      v-if="totalAnsweredQuestion < quizQuestions.length"
        :totalQuestionsAnswered="totalAnsweredQuestion"
        :questions="quizQuestions"
        @answered="answered"
      />
      <Result v-else :results="results" :totalCorrectAnswer="totalCorrectAnswer"/>
    </transition>

    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="totalAnsweredQuestion === quizQuestions.length"
    >
      Reset
    </button>
  </div>
  
</template>
