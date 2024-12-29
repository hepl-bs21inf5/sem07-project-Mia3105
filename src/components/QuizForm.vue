<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'
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

const questionRadiooptionsshuffle1 = ref(
  shuffleArray([
    { value: '3.1514131211', text: '3.1514131211' },
    { value: '3.1415926535', text: '3.1415926535' },
    { value: '3.1415996633', text: '3.1415996633' },
    { value: '1.1415926535', text: '1.1415926535' },
  ]),
)

const questionRadiooptionsshuffle2 = ref(
  shuffleArray([
    { value: 'Théorème de Thalès', text: 'Théorème de Thalès' },
    { value: 'Théorème des deux gendarmes', text: 'Théorème des deux gendarmes' },
    { value: 'Théorème de Pythagore', text: 'Théorème de Pythagore' },
    { value: 'Théorème de Cauchy', text: 'Théorème de Cauchy' },
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
  questionRadiooptionsshuffle1.value = shuffleArray(questionRadiooptionsshuffle1.value)
  questionRadiooptionsshuffle2.value = shuffleArray(questionRadiooptionsshuffle2.value)
}
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
    <QuestionSelect
      id="jour"
      v-model="questionStates[0]"
      answer="a"
      text="1. Quelle est la première lettre de l'alphabet ?"
      placeholder="Veuillez choisir une option"
      :options="[
        { value: 'a', text: 'a' },
        { value: 'e', text: 'e' },
        { value: 'i', text: 'i' },
        { value: 'o', text: 'o' },
        { value: 'u', text: 'u' },
        { value: 'y', text: 'y' },
      ]"
      answer-detail="C'est a."
    />

    <br />
    <QuestionRadio
      id="pi"
      v-model="questionStates[1]"
      answer="3.1415926535"
      text="2. Quelles sont les 10 premières décimales de π ?"
      :options="questionRadiooptionsshuffle1"
      answer-detail="Que (3) j' (1) aime (4) à (1) faire (5) apprendre (9) ce (2) nombre (6) utile (5) aux (3) sages (5)."
    />

    <br />

    <QuestionText
      id="planète"
      v-model="questionStates[2]"
      :answer="['8', 'huit', 'Huit']"
      text="3. Combien y a-t-il de planètes dans le système solaire ?"
      placeholder="Veuillez saisir un nombre"
      answer-detail="Les 8 planètes sont Mercure, Venus, Terre, Mars, Jupiter, Saturne, Uranus, Neptune. Pluton n'est plus considérée comme une planète depuis 2006."
    />

    <br />

    <QuestionRadio
      id="theoreme"
      v-model="questionStates[3]"
      answer="Théorème de Pythagore"
      text="4. Quel théorème est utilisé uniquement dans les triangles rectangles ?"
      :options="questionRadiooptionsshuffle2"
      answer-detail="Le théorème de Pythagore permet de faire un lien entre les angles et les longueurs dans un triangle rectangle."
    />

    <br /><br />
    <div
      style="
        position: fixed;
        top: 85px;
        right: 0px;
        width: 200px;
        background: white;
        text-align: left;
        padding: 10px;
        border: 1px solid rgb(241, 241, 241);
        box-shadow: rgba(0, 0, 0, 0.2) 0px 2px 4px;
        line-height: 20px;
        margin: 10px;
        outline: 0px;
      "
    >
      Aperçu des questions :
      <br />
      <div v-for="(state, index) in questionStates" :key="index">{{ index + 1 }}. {{ state }}</div>
    </div>

    <div style="text-align: left">
      <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    </div>

    <div style="text-align: right">
      <button class="btn btn-primary" @:click="reset">Réinitialiser</button>
    </div>
    <br />
  </form>
</template>
