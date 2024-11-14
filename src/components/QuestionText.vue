<script setup lang="ts">
import { defineModel, defineProps } from 'vue'

const reponse = defineModel<string | null>()
const props = defineProps({
  id: { type: String, required: true },
  text: { type: String, required: true },
  placeholder: { type: String, required: true },
})
</script>

<template>
  <label for="props.id" class="form-label"></label>
  {{ props.text }}
  <input
    :id="`${props.id}`"
    v-model="reponse"
    class="form-control"
    :name="props.id"
    :placeholder="props.placeholder"
  />
</template>
