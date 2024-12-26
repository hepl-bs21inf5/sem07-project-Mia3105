<script setup lang="ts">
  import QuestionRadio from "@/components/QuestionRadio.vue";
  import { computed, ref } from "vue";
  import { QuestionState } from '@/utils/models'

  const questions = ref<
    {
      question: string;
      correct_answer: string;
      incorrect_answers: string[];
      answer: string ;
    }[]
  >([]);

const questionStates = ref<QuestionState[]>([])

const filled = computed<boolean>(() =>
  questionStates.value.every((state) => state === QuestionState.Fill),
)

const submitted = computed<boolean>(() =>
  questionStates.value.every(
    (state) => state === QuestionState.Correct || state === QuestionState.Wrong,
  ),
)

const score = computed<number>(
  () => questionStates.value.filter((state) => state === QuestionState.Correct).length,
)

const totalScore = computed<number>(() => questionStates.value.length)



function submit(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Submit)
  document.body.scrollTop = 0
  document.documentElement.scrollTop = 0
}

function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Empty)
  document.body.scrollTop = 0
  document.documentElement.scrollTop = 0
}



  fetch("https://opentdb.com/api.php?amount=10&type=multiple")
    .then((response) => response.json())
    .then((data) => (questions.value = data.results));
</script>

<template>
  <form @submit="submit">
    <br />
    <div
      v-if="submitted"
      style="width: 110px; background: #0080ff; padding: 10px; color: white; border-radius: 10px"
    >
      Score : {{ score }} / {{ totalScore }}
    </div>
    <br />
    <QuestionRadio
      v-for="(question, index) in questions"
      :id="index.toString()"
      :key="index"
      :answer="question.answer"
      :text="question.question"
      :options="[
        { value: question.correct_answer, text: question.correct_answer },
        ...question.incorrect_answers.map(answer => ({
          value: answer,
          text: answer,
        })),
      ]"
    />

    <div style="text-align: left">
      <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    </div>

    <div style="text-align: right">
      <button class="btn btn-primary" button @:click="reset">Réinitialiser</button>
    </div>
    <br />


  </form>
</template>
