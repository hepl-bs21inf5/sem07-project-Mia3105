<script setup lang="ts">
import { computed, ref } from 'vue'
import QuestionRadio from '@/components/QuestionRadio.vue'
import QuestionText from '@/components/QuestionText.vue'
import QuestionCheckbox from '@/components/QuestionCheckbox.vue'

const cheval = ref<string | null>(null)
const chat = ref<string | null>(null)
const capitale = ref<string | null>(null)
const lausanne = ref<string[]>([])
const correctAnswers = ref<boolean[]>([])
const score = computed<number>(() => correctAnswers.value.filter((value) => value).length)
const totalScore = computed<number>(() => correctAnswers.value.length)

const filled = computed<boolean>(
  () =>
    cheval.value !== null &&
    chat.value !== null &&
    capitale.value !== null &&
    lausanne.value !== [],
)

function submit(event: Event): void {
  event.preventDefault()

  if (filled.value) {
    alert(`
    Vous avez choisi la couleur ${cheval.value}
    Vous avez choisi ${chat.value}
    Vous avez choisi la ville de ${capitale.value}
    Vous avez choisi ${lausanne.value}
    `)
  }
}

function refresh(event: Event): void {
  event.preventDefault()
  cheval.value = null
  chat.value = null
  capitale.value = null
  lausanne.value = []
}
</script>

<template>
  <form>
    <QuestionRadio
      id="cheval"
      v-model="correctAnswers[0]"
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
      v-model="correctAnswers[1]"
      answer="4"
      text="Combien de pattes a un chat ?"
      placeholder="Veuillez saisir un nombre"
    />

    <br />

    <QuestionRadio
      id="capitale"
      v-model="correctAnswers[2]"
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
      v-model="lausanne"
      text="Où se situe Lausanne ?"
      :options="[
        { value: 'Canton de Vaud', text: 'Canton de Vaud' },
        { value: 'en Suisse', text: 'en Suisse' },
        { value: 'Canton du Valais', text: 'Canton du Valais' },
        { value: 'en France', text: 'en France' },
      ]"
    />

    <br />
    <br />

    <div>Réponses correctes : {{ correctAnswers }}</div>
    <div>Score : {{ score }} / {{ totalScore }}</div>

    <br />
    <br />
  </form>

  <form @submit="submit">
    <button class="btn btn-primary" :class="{ disabled: !filled }" type="submit">Terminer</button>
    <button style="margin-left: 10em" class="btn btn-primary" button @:click="refresh">
      Réinitialiser
    </button>
  </form>
</template>
