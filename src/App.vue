<script setup lang="ts">
import PrimaryButton from "./components/PrimaryButton.vue";
import StrengthIndicator from "./components/StrengthIndicator.vue";
import IconArrowRight from "./components/icons/IconArrowRight.vue";
</script>

<template>
  <main>
    <h1>Password Generator</h1>
    <div>
      <StrengthIndicator :strength="4" />
      <PrimaryButton :end-icon="IconArrowRight">Generate</PrimaryButton>
    </div>
  </main>
</template>

<style>
main {
  width: min(100% - 2rem, 540px);
  margin-inline: auto;
}

main > div {
  background-color: var(--color-foreground);
  padding: 2rem;
  padding-top: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}
</style>
