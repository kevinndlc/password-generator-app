<script setup lang="ts">
import { computed } from "vue";

const props = defineProps<{
  strength: 1 | 2 | 3 | 4;
}>();

const strengthText = computed(() => {
  switch (props.strength) {
    case 1:
      return "Too weak!";
    case 2:
      return "Weak";
    case 3:
      return "Medium";
    case 4:
      return "Strong";
    default:
      return "Unknown";
  }
});

const strengthColor = computed(() => {
  switch (props.strength) {
    case 1:
      return "var(--color-too-weak)";
    case 2:
      return "var(--color-weak)";
    case 3:
      return "var(--color-medium)";
    case 4:
      return "var(--color-strong)";
    default:
      return "white";
  }
});
</script>

<template>
  <div class="wrapper">
    <span>Strength</span>
    <div>
      <h2>{{ strengthText }}</h2>
      <div class="strength-squares">
        <div
          v-for="sq in Array(4).keys()"
          :key="sq"
          :class="strength >= sq + 1 && 'active'"
        ></div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.wrapper {
  background-color: var(--color-background);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

span {
  text-transform: uppercase;
  color: var(--color-text-muted);
}

.wrapper > div {
  display: flex;
  align-items: center;
  gap: 1rem;
}

h2 {
  text-transform: uppercase;
}

.strength-squares {
  display: flex;
  gap: 0.5rem;
}

.strength-squares > div {
  width: 10px;
  height: 28px;
  border: 2px solid;
}

.strength-squares > .active {
  color: v-bind(strengthColor);
  background-color: v-bind(strengthColor);
}
</style>
