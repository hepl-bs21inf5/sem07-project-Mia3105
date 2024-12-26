<script setup lang="ts">
import { defineModel, defineProps, watch, ref } from 'vue'
import { QuestionState } from '@/utils/models'

const reponse = defineModel<QuestionState>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  placeholder: { type: String, required: true },
  answerDetail: { type: String, default: '' },
})

const value = ref<string | null>(null)

watch(reponse, (newModel) => {
  if (newModel === QuestionState.Submit) {
    reponse.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    value.value = null
  }
})

watch(
  value,
  (newValue) => {
    if (newValue === null) {
      reponse.value = QuestionState.Empty
    } else {
      reponse.value = QuestionState.Fill
    }
  },
  { immediate: true },
)
</script>

<template>
  <label for="props.id" class="form-label"></label>
  {{ props.text }}
  <input
    :id="`${props.id}`"
    v-model="value"
    :answer="props.answer"
    class="form-control"
    :name="props.id"
    :placeholder="props.placeholder"
    :disabled="
      reponse === QuestionState.Submit ||
      reponse === QuestionState.Correct ||
      reponse === QuestionState.Wrong
    "
  />
  <div v-if="reponse === QuestionState.Correct || reponse === QuestionState.Wrong">
    <p v-if="reponse === QuestionState.Correct" class="text-success">Juste !</p>
    <p v-else class="text-danger">Faux ! La réponse était : {{ answer }}</p>
    <p class="blockquote-footer">{{ props.answerDetail }}</p>
  </div>
</template>

<style scoped>
.text-danger {
  color: rgb(248, 49, 47) !important;
}
.text-success {
  color: rgb(0, 210, 106) !important;
}
</style>

