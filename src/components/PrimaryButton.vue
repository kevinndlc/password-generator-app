<script setup lang="ts">
defineProps<{
  endIcon?: Node;
}>();
</script>

<template>
  <button>
    <slot />
    <component :is="endIcon" />
  </button>
</template>

<style scoped>
button {
  background-color: var(--color-strong);
  text-transform: uppercase;
  display: inline-flex;
  justify-content: center;
  gap: 1.5rem;
  align-items: center;
  height: 4rem;
  width: 100%;
  border: 2px solid transparent;
  transition: 200ms ease-in-out;
}

button:hover {
  background-color: transparent;
  color: var(--color-strong);
  border-color: var(--color-strong);
}
</style>
