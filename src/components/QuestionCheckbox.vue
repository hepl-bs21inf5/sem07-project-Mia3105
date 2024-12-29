<script setup lang="ts">
import { ref, defineProps, type PropType, watch } from 'vue'
import { QuestionState } from '@/utils/models';

const checkedNames = ref<QuestionState>();
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: Array as PropType<Array<string>>, required: true },
  options: {
    type: Array as PropType<Array<{ value: string; text: string }>>,
    required: true,
  },
})


  const value = ref([])

  watch(checkedNames, (newModel) => {
  if (newModel === QuestionState.Submit) {
    checkedNames.value = value.value === props.answer ? QuestionState.Correct : QuestionState.Wrong
  } else if (newModel === QuestionState.Empty) {
    value.value = []
  }
})

watch(
  value,
  (newValue) => {
    if (newValue === null) {
      checkedNames.value = QuestionState.Empty
    } else {
      checkedNames.value = QuestionState.Fill
    }
  },
  { immediate: true },
)


</script>

<template>
  {{ props.text }}
  <div v-for="option in props.options" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"
      v-model="value"
      class="form-check-input"
      type="checkbox"
      answer="props.value"
      :name="props.id"
      :value="option.value"
      :disabled="
        checkedNames === QuestionState.Submit ||
        checkedNames === QuestionState.Correct ||
        checkedNames === QuestionState.Wrong
        "
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
</template>
