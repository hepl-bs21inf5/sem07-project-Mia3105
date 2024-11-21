<script setup lang="ts">
import { defineModel, defineProps, watch, ref } from 'vue'

const reponse = defineModel<boolean>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  answer: { type: String, required: true },
  placeholder: { type: String, required: true },
})


const value = ref<string | null>(null);

  watch(
    value,
    (newValue) => {
      reponse.value = newValue === props.answer;
    },
    { immediate: true },
  );


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

  />
</template>
