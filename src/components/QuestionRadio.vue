<script setup lang="ts">
  import { defineModel, defineProps, type PropType } from "vue";

  const model = defineModel<string | null>();
  const props = defineProps({
    id: { type: String, required: true },
    text: { type: String, required: true },
    options: {
      type: Array as PropType<Array<{ value: string; text: string }>>,
      required: true,
    },
  });
</script>

<template>
  {{ props.text }}
  <div v-for="option in props.options" :key="option.value" class="form-check">
    <input
      :id="`${props.id}-${option.value}`"      
      v-model="model"
      class="form-check-input"
      type="radio"
      :name="props.id"
      :value="option.value"
    />
    <label class="form-check-label" :for="`${props.id}-${option.value}`">
      {{ option.text }}
    </label>
  </div>
</template>
