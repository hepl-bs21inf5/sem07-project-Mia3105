<script setup lang="ts">
import QuestionRadio from '@/components/QuestionRadio.vue'
import { computed, ref, watch, defineModel } from 'vue'
import { QuestionState } from '@/utils/models'

const questions = ref<
  {
    question: string
    correct_answer: string
    incorrect_answers: string[]
    answer: string
  }[]
>([])

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

function reload(event: Event): void {
  event.preventDefault()
  location.reload()
  document.body.scrollTop = 0
  document.documentElement.scrollTop = 0
}

fetch('https://opentdb.com/api.php?amount=10&type=multiple')
  .then((response) => response.json())
  .then((data) => (questions.value = data.results))

const model = defineModel<QuestionState>()
const value = ref<string | null>(null)

watch(
  value,
  (newValue) => {
    if (newValue === null) {
      model.value = QuestionState.Empty
    } else {
      model.value = QuestionState.Fill
    }
  },
  { immediate: true },
)
</script>

<template>
  <form @submit="submit">
    <br />
    <div
      v-if="submitted"
      style="width: 125px; background: #008cff; padding: 10px; color: white; border-radius: 10px"
    >
      Score : {{ score }} / {{ totalScore }}
    </div>
    <br />
    <div v-if="score == totalScore" style="font-size: x-large; font-weight: bold">
      <img src="https://images.emojiterra.com/mozilla/1024px/1f389.png" width="100px" />
      &nbsp; &nbsp; BRAVO !! &nbsp; &nbsp;
      <img src="https://images.emojiterra.com/mozilla/1024px/1f389.png" width="100px" />
      &nbsp; &nbsp;
      <img
        src="https://images.emojiterra.com/google/noto-emoji/unicode-16.0/color/1024px/1f44f.png"
        width="100px"
      />
    </div>
    <br />
    <div v-for="(question, index) in questions" :key="index" class="box_question">
      <QuestionRadio
        :id="index.toString()"
        :key="index"
        v-model="questionStates[index]"
        :answer="question.correct_answer"
        :text="index + 1 + '. ' + question.question"
        :options="[
          { value: question.correct_answer, text: question.correct_answer },
          ...question.incorrect_answers.map((answer) => ({
            value: answer,
            text: answer,
          })),
        ]"
      />
    </div>

    <br /><br />
    <div class="box_satut_questions">
      Aperçu des questions:
      <br />
      <div style="display: flex; gap: 10px; flex-wrap: wrap; align-items: center">
        <!-- Permet que les aperçus s'affichent  en ligne et reviennent à la ligne quand la ligne est pleine -->
        <div v-for="(state, index) in questionStates" :key="index">
          {{ index + 1 }}. {{ state }}
        </div>
      </div>
    </div>

    <br />
    <div style="text-align: left">
      <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    </div>

    <div style="text-align: right">
      <button class="btn btn-primary" @:click="reset">Réinitialiser</button>
      &nbsp; &nbsp;
      <button class="btn btn-primary" @:click="reload">Générer de nouvelles questions</button>
    </div>
    <br /><br /><br /><br /><br /><br /><br />
  </form>
</template>

<style scoped>
.box_question {
  border: 2px solid rgb(238, 247, 252);
  border-radius: 10px;
  background: rgb(238, 247, 252);
  padding: 20px;
  margin-bottom: 25px;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px;
}

.box_satut_questions {
  position: fixed;
  top: 5%;
  right: 0px;
  width: 40%;
  border-radius: 10px;
  background: rgb(245, 245, 245);
  text-align: left;
  padding: 10px;
  border: 1px solid rgb(241, 241, 241);
  box-shadow: rgba(0, 0, 0, 0.2) 0px 2px 4px;
  line-height: 20px;
  margin: 10px;
  outline: 0px;
}

@media (max-width: 745px) {
  .box_satut_questions {
    top: auto;
    bottom: 30px;
    left: 0;
    right: 0;
    width: 100%;
  }
}
</style>
