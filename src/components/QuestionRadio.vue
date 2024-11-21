<script setup lang="ts">
import { defineModel, defineProps, type PropType, ref, watch } from 'vue'

  const model = defineModel<boolean>()
  const props = defineProps({
    id: { type: String, required: true },
    text: { type: String, required: true },
    answer: { type: String, required: true },
    options: {
      type: Array as PropType<Array<{ value: string; text: string }>>,
      required: true,
    },

  })

  const value = ref<string | null>(null)

  watch(value, (newValue) => {
      model.value = newValue === props.answer
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
      type="radio"
      :name="props.id"
      :value="option.value"
      :anwser="props.answer"
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
</template>
