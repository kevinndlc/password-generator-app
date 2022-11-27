<script setup lang="ts">
import PrimaryButton from "./components/PrimaryButton.vue";
import StrengthIndicator from "./components/StrengthIndicator.vue";
import IconArrowRight from "./components/icons/IconArrowRight.vue";
import GeneratedPassword from "./components/GeneratedPassword.vue";
</script>

<template>
  <main>
    <h1>Password Generator</h1>
    <GeneratedPassword password="pIkAchuuuu" class="generated-pw" />
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
</style>

<style scoped>
h1 {
  text-align: center;
  color: var(--color-text-muted);
  font-size: 1.5rem;
  margin-bottom: 2rem;
}

main > div {
  background-color: var(--color-foreground);
  padding: 2rem;
  padding-top: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.generated-pw {
  margin-bottom: 1.5rem;
}
</style>
