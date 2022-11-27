<script setup lang="ts">
import PrimaryButton from "./components/PrimaryButton.vue";
import StrengthIndicator from "./components/StrengthIndicator.vue";
import IconArrowRight from "./components/icons/IconArrowRight.vue";
import GeneratedPassword from "./components/GeneratedPassword.vue";
import LengthSlider from "./components/LengthSlider.vue";
import { computed, ref } from "vue";
import CheckboxInput from "./components/CheckboxInput.vue";

const LOWERCASE_LETTERS = "abcdefghijklmnopqrstuvwxyz";
const UPPERCASE_LETTERS = LOWERCASE_LETTERS.toUpperCase();
const NUMBERS = "0123456789";
const SYMBOLS = "?!$&#_";

const passwordOptions = ref<string[]>([]);

const generatedPassword = ref("");
const passwordLength = ref(8);
const passwordStrength = computed<0 | 1 | 2 | 3 | 4>(() => {
  if (!passwordOptions.value.length) return 0;
  if (passwordLength.value <= 4) return 1;

  let min = 0;

  if (passwordLength.value <= 8) {
    min = 1;
  } else if (passwordLength.value > 8 && passwordLength.value <= 12) {
    min = 2;
  } else if (passwordLength.value > 12 && passwordLength.value <= 16) {
    min = 3;
  } else {
    min = 4;
  }
  return Math.max(passwordOptions.value.length, min) as 1 | 2 | 3 | 4;
});

function generateRandomPassword() {
  const choices = [];

  if (passwordOptions.value.includes("uppercase")) {
    choices.push(...UPPERCASE_LETTERS);
  }
  if (passwordOptions.value.includes("lowercase")) {
    choices.push(...LOWERCASE_LETTERS);
  }
  if (passwordOptions.value.includes("numbers")) {
    choices.push(...NUMBERS);
  }
  if (passwordOptions.value.includes("symbols")) {
    choices.push(...SYMBOLS);
  }

  if (!choices.length) return;

  let newPassword = "";

  for (let i = 0; i < passwordLength.value; i++) {
    const randomChar = choices[Math.floor(Math.random() * choices.length)];
    newPassword += randomChar;
  }

  generatedPassword.value = newPassword;
}
</script>

<template>
  <main>
    <h1>Password Generator</h1>
    <GeneratedPassword :password="generatedPassword" class="generated-pw" />
    <div>
      <LengthSlider
        :length="passwordLength"
        @update-length="(length) => (passwordLength = length)"
      />
      <div class="checklist">
        <CheckboxInput
          @update:model-value="
            (value) => {
              passwordOptions.includes(value)
                ? passwordOptions.splice(passwordOptions.indexOf(value), 1)
                : passwordOptions.push(value);
            }
          "
          group="options"
          id="uppercase"
          label="Include Uppercase Letters"
        />
        <CheckboxInput
          @update:model-value="
            (value) => {
              passwordOptions.includes(value)
                ? passwordOptions.splice(passwordOptions.indexOf(value), 1)
                : passwordOptions.push(value);
            }
          "
          group="options"
          id="lowercase"
          label="Include Lowercase Letters"
        />
        <CheckboxInput
          @update:model-value="
            (value) => {
              passwordOptions.includes(value)
                ? passwordOptions.splice(passwordOptions.indexOf(value), 1)
                : passwordOptions.push(value);
            }
          "
          group="options"
          id="numbers"
          label="Include Numbers"
        />
        <CheckboxInput
          @update:model-value="
            (value) => {
              passwordOptions.includes(value)
                ? passwordOptions.splice(passwordOptions.indexOf(value), 1)
                : passwordOptions.push(value);
            }
          "
          group="options"
          id="symbols"
          label="Include Symbols"
        />
      </div>
      <StrengthIndicator :strength="passwordStrength" />
      <PrimaryButton :end-icon="IconArrowRight" @click="generateRandomPassword"
        >Generate</PrimaryButton
      >
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

.checklist {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}
</style>
