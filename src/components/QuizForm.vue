<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'
import { QuestionState } from '@/utils/models'

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
}

function reset(event: Event): void {
  event.preventDefault()
  questionStates.value = questionStates.value.map(() => QuestionState.Empty)
}
</script>

<template>
  <form>
    <QuestionRadio
      id="cheval"
      v-model="questionStates[0]"
      answer="blanc"
      text="De quelle couleur est le cheval blanc de Napoléon ?"
      :options="[
        { value: 'blanc', text: 'Blanc' },
        { value: 'brun', text: 'Brun' },
        { value: 'noir', text: 'Noir' },
        { value: 'rouge', text: 'Rouge' },
      ]"
    />

    <br />

    <QuestionText
      id="chat"
      v-model="questionStates[1]"
      answer="4"
      text="Combien de pattes a un chat ?"
      placeholder="Veuillez saisir un nombre"
    />

    <br />

    
    <QuestionRadio
      id="capitale"
      v-model="questionStates[2]"
      answer="Berne"
      text="Quelle est la capitale de la Suisse ?"
      :options="[
        { value: 'Geneve', text: 'Genève' },
        { value: 'Lausanne', text: 'Lausanne' },
        { value: 'Berne', text: 'Berne' },
        { value: 'Zurich', text: 'Zurich' },
      ]"
    />

    <br />

    <QuestionCheckbox
      id="lausanne"
      v-model="questionStates[3]"
      text="Où se situe Lausanne ?"
      answer="..."
      :options="[
        { value: 'Canton de Vaud', text: 'Canton de Vaud' },
        { value: 'en Suisse', text: 'en Suisse' },
        { value: 'Canton du Valais', text: 'Canton du Valais' },
        { value: 'en France', text: 'en France' },
      ]"
    />

    <br />
    <br />

    <div>Debug états : {{ questionStates }}</div>
    <div v-if="submitted">Score : {{ score }} / {{ totalScore }}</div>
    <br />
    <br />
  </form>

  <form @submit="submit">
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <button style="margin-left: 10em" class="btn btn-primary" button @:click="reset">
      Réinitialiser
    </button>
  </form>
</template>
