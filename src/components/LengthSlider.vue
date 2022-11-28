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
    <div class="input-container" :style="`--progress: ${(length / 20) * 100}%`">
      <input
        type="range"
        :value="length"
        @input="
          emit(
            'updateLength',
            parseInt(($event.target as HTMLInputElement).value)
          )
        "
        min="1"
        max="20"
      />
      <div></div>
    </div>
  </div>
</template>

<style scoped>
.wrapper > div {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1rem;
}

.wrapper > div .number {
  color: var(--color-strong);
  font-size: 2rem;
}

.wrapper input[type="range"] {
  width: 100%;
  opacity: 0;
  height: 8px;
  position: relative;
  z-index: 9;
}

.input-container {
  position: relative;
}

.input-container > div {
  position: absolute;
  inset: 0;
  background-color: var(--color-background);
}

.input-container > div::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: var(--progress);
  background-color: var(--color-strong);
}

.input-container > div::after {
  content: "";
  position: absolute;
  top: 50%;
  left: var(--progress);
  height: 28px;
  aspect-ratio: 1;
  border-radius: 50%;
  transform-box: border-box;
  transform: translate(-80%, -50%);
  background-color: var(--color-text);
}

.input-container:focus-within > div::after {
  border: 2px solid var(--color-strong);
}
</style>
