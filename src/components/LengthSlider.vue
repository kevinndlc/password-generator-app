<script setup lang="ts">
defineProps<{
  length: number;
}>();

const emit = defineEmits<{
  (e: "updateLength", length: number): void;
}>();
</script>

<template>
  <div class="wrapper">
    <div>
      <span class="text">Character Length</span>
      <span class="number">{{ length }}</span>
    </div>
    <input
      type="range"
      value="length"
      @input="
        emit(
          'updateLength',
          parseInt(($event.target as HTMLInputElement).value)
        )
      "
      min="1"
      max="20"
    />
  </div>
</template>

<style scoped>
.wrapper > div {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.wrapper > div .number {
  color: var(--color-strong);
}

.wrapper input[type="range"] {
  width: 100%;
}
</style>
