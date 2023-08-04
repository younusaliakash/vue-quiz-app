<script setup>
import { defineProps, computed } from "vue";

const { results, totalCorrectAnswer } = defineProps([
  "results",
  "totalCorrectAnswer",
]);

const resultIndex = computed(() => {
  let index = 0;

  results.forEach((e, i) => {
    if (e.min <= totalCorrectAnswer && e.max >= totalCorrectAnswer) {
      index = i;
    }
  });

  return index;
});
</script>

<template>
  <div class="result">
    <div class="title">{{ results[resultIndex].title }}</div>
    <div class="desc">{{ results[resultIndex].desc }}</div>
  </div>
</template>

<style scoped></style>
