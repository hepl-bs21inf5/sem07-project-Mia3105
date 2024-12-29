<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import { QuestionState } from '@/utils/models'
import QuestionSelect from './QuestionSelect.vue'

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

function shuffleArray<T>(array: T[]): T[] {
  const shuffled = [...array]
  for (let i = shuffled.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
    ;[shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]]
  }
  return shuffled
}

const questionRadio_options_shuffle1 = ref(
  shuffleArray([
    { value: '3.1514131211', text: '3.1514131211' },
    { value: '3.1415926535', text: '3.1415926535' },
    { value: '3.1415996633', text: '3.1415996633' },
    { value: '1.1415926535', text: '1.1415926535' },
  ]),
)

const questionRadio_options_shuffle2 = ref(
  shuffleArray([
    { value: 'thalès', text: 'Théorème de Thalès' },
    { value: 'gendarmes', text: 'Théorème des deux gendarmes' },
    { value: 'pythagore', text: 'Théorème de Pythagore' },
    { value: 'cauchy', text: 'Théorème de Cauchy' },
  ]),
)

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
  questionRadio_options_shuffle1.value = shuffleArray(questionRadio_options_shuffle1.value)
  questionRadio_options_shuffle2.value = shuffleArray(questionRadio_options_shuffle2.value)
}
</script>

<template>
  <form @submit="submit">
    <br />
    <div
      v-if="submitted"
      style="width: 110px; background: #008cff; padding: 10px; color: white; border-radius: 10px"
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
    <div class="box_question">
      <QuestionSelect
        id="premier"
        v-model="questionStates[0]"
        answer="2"
        text="1. Quel est le premier nombre premier ?"
        :options="[
          { value: '5', text: '5' },
          { value: '2', text: '2' },
          { value: '7', text: '7' },
          { value: '3', text: '3' },
        ]"
        answer-detail="Le premier nombre premier est 2."
      />
    </div>

    <div class="box_question">
      <QuestionRadio
        id="pi"
        v-model="questionStates[1]"
        answer="3.1415926535"
        text="2. Quelles sont les 10 premières décimales de π ?"
        :options="questionRadio_options_shuffle1"
        answer-detail="Voilà une phrase pour s'en souvenir : Que (3) j' (1) aime (4) à (1) faire (5) apprendre (9) ce (2) nombre (6) utile (5) aux (3) sages (5)."
      />
    </div>

    <div class="box_question">
      <QuestionText
        id="planète"
        v-model="questionStates[2]"
        :answer="['8', 'huit', 'Huit']"
        text="3. Combien y a-t-il de planètes dans le système solaire ?"
        placeholder="Veuillez saisir un nombre"
        answer-detail="Les 8 planètes sont Mercure, Venus, Terre, Mars, Jupiter, Saturne, Uranus, Neptune. Pluton n'est plus considérée comme une planète depuis 2006."
      />
    </div>

    <div class="box_question">
      <QuestionRadio
        id="theoreme"
        v-model="questionStates[3]"
        answer="pythagore"
        text="4. Quel théorème est utilisé uniquement dans les triangles rectangles ?"
        :options="questionRadio_options_shuffle2"
        answer-detail="Le théorème de Pythagore permet de faire un lien entre les angles et les longueurs dans un triangle rectangle."
      />
    </div>

    <br />
    <div class="box_satut_questions">
      Aperçu des questions:
      <br />
      <div style="display: flex; gap: 10px; flex-wrap: wrap; align-items: center">
        <!-- Permet que les aperçus s'affichent en ligne et reviennent à la ligne quand la ligne est pleine -->
        <div v-for="(state, index) in questionStates" :key="index">
          {{ index + 1 }}. {{ state }}
        </div>
      </div>
    </div>

    <div style="text-align: left">
      <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    </div>

    <div style="text-align: right">
      <button class="btn btn-primary" @:click="reset">Réinitialiser</button>
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
