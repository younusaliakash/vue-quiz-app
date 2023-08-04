<script setup>
import { defineProps } from "vue";

const { questions, totalQuestionsAnswered } = defineProps([
  "totalQuestionsAnswered",
  "questions",
]);

const emit = defineEmits(["answered"]);

const selectAnswer = (is_correct) => {
  emit("answered", is_correct);
};
</script>

<template>
  <div class="questions-ctr">
    <div class="progress">
      <div
        class="bar"
        :style="{
          width: `${(totalQuestionsAnswered / questions.length) * 100}%`,
        }"
      ></div>
      <div class="status">
        {{ totalQuestionsAnswered }} out of {{ questions.length }} Questions
        Answered
      </div>
    </div>
    <transition-group name="fade">
      <div
        class="single-question"
        v-for="(question, idx) in questions"
        :key="idx"
        v-show="totalQuestionsAnswered === idx"
      >
        <div class="question">{{ question.q }}</div>
        <div class="answers">
          <div
            class="answer"
            v-for="(answer, idax) in question.answers"
            :key="idax"
            @click="selectAnswer(answer.is_correct)"
          >
            {{ answer.text }}
          </div>
        </div>
      </div>
    </transition-group>
  </div>
</template>

<!-- <template>
    <div class="questions-ctr">
      <div class="progress">
        <div
          class="bar"
          :style="{ width: `${(questionsAnswered / questions.length) * 100}%` }"
        ></div>
        <div class="status">
          {{ questionsAnswered }} out of {{ questions.length }} questions answered
        </div>
      </div>
      <transition-group name="fade">
        <div
          class="single-question"
          v-for="(question, qi) in questions"
          :key="question.q"
          v-show="questionsAnswered === qi"
        >
          <div class="question">{{ question.q }}</div>
          <div class="answers">
            <div
              class="answer"
              v-for="answer in question.answers"
              :key="answer.text"
              @click.prevent="selectAnswer(answer.is_correct)"
            >
              {{ answer.text }}
            </div>
          </div>
        </div>
      </transition-group>
    </div>
  </template> -->
