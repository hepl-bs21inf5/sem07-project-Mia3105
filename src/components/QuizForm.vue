<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'
import { QuestionState } from '@/utils/models'

const questionStates = ref<QuestionState[]>([])

const filled = computed<boolean>(() =>
  questionStates.value.every((state) => state === QuestionState.Remplie),
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
}

function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Vide)
}
</script>

<template>
  <form @submit="submit">
    <div class="container">
      <div class="row">
        <div class="col">
          <QuestionRadio
            id="pi"
            v-model="questionStates[0]"
            answer="3.1415926535"
            text="Quelles sont les 10 premières décimales de π ?"
            :options="[
              { value: '3.1514131211', text: '3.1514131211' },
              { value: '3.1415926535', text: '3.1415926535' },
              { value: '3.1415996633', text: '3.1415996633' },
              { value: '1.1415926535', text: '1.1415926535' },
            ]"
            answer-detail="Que (3) j' (1) aime (4) à (1) faire (5) apprendre (9) ce (2) nombre (6) utile (5) aux (3) sages (5)."
          />

          <br />

          <QuestionText
            id="planète"
            v-model="questionStates[1]"
            answer="8"
            text="Combien y a-t-il de planètes dans le système solaire ?"
            placeholder="Veuillez saisir un nombre"
            answer-detail="Les 8 planètes sont Mercure, Venus, Terre, Mars, Jupiter, Saturne, Uranus, Neptune. Pluton n'est plus considéré comme une planète."
          />

          <br />

          <QuestionRadio
            id="theoreme"
            v-model="questionStates[2]"
            answer="Théorème de Pythagore"
            text="Quel théorème est utilisé uniquement dans les triangles rectangles ?"
            :options="[
              { value: 'Théorème de Thalès', text: 'Théorème de Thalès' },
              { value: 'Théorème des deux gendarmes', text: 'Théorème des deux gendarmes' },
              { value: 'Théorème de Pythagore', text: 'Théorème de Pythagore' },
              { value: 'Théorème de Cauchy', text: 'Théorème de Cauchy' },
            ]"
            answer-detail="Le théorème de Pythagore permet de faire un lien entre les angles et les longueurs dans un triangle rectangle."
          />

          <br />

          <QuestionCheckbox
            id="lausanne"
            v-model="questionStates[3]"
            text="Où se situe Lausanne ?"
            :answer="['Canton de Vaud', 'en Suisse']"
            :options="[
              { value: 'Canton de Vaud', text: 'Canton de Vaud' },
              { value: 'en Suisse', text: 'en Suisse' },
              { value: 'Canton du Valais', text: 'Canton du Valais' },
              { value: 'en France', text: 'en France' },
            ]"
          />

          <br />
          <br />
          <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">
            Terminer
          </button>
        </div>

        <div class="col">
          <div> États des questions : {{ questionStates }}</div>
          <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
          <br />
          <br />

          <br />
          <br />
          <div style="text-align: right">
            <button class="btn btn-primary" button @:click="reset">Réinitialiser</button>
          </div>
        </div>
      </div>
    </div>
  </form>
</template>
