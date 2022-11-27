<script setup lang="ts">
import StrengthIndicator from './components/StrengthIndicator.vue';

</script>

<template>
  <main>
    <h1>Password Generator</h1>
    <StrengthIndicator :strength="4" />
  </main>
</template>

<style>
main {
  width: min(100% - 2rem, 540px);
  margin-inline: auto;
  background-color: var(--color-foreground);
}
</style>
