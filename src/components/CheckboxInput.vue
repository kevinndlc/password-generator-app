<script setup lang="ts">
import IconCheck from "./icons/IconCheck.vue";

defineProps<{
  group: string;
  id: string;
  label?: string;
}>();

const emit = defineEmits<{
  (e: "update:modelValue", checkedBox: string): void;
}>();
</script>

<template>
  <div class="wrapper">
    <input
      ref="input"
      type="checkbox"
      :value="id"
      @input="
        emit('update:modelValue', ($event.target as HTMLInputElement).value)
      "
      :name="group"
      :id="id"
    />
    <label v-if="label" :for="id">{{ label }}</label>
    <button
      @click="() => {
        ($refs.input as HTMLInputElement).checked = !($refs.input as HTMLInputElement).checked
        emit('update:modelValue', id);
      }
      "
    >
      <span class="sr-only">Check</span>
      <IconCheck />
    </button>
  </div>
</template>

<style scoped>
.wrapper {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

input {
  display: none;
}

button {
  padding: 0;
  display: grid;
  place-content: center;
  order: 1;
  width: 20px;
  aspect-ratio: 1;
  border: 2px solid;
}

button > svg {
  display: none;
}

input:checked ~ button {
  background-color: var(--color-strong);
  border-color: var(--color-strong);
  color: var(--color-background);
}
input:checked ~ button > svg {
  display: revert;
}

label {
  order: 2;
  user-select: none;
  cursor: pointer;
}
</style>
