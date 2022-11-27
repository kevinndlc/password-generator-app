<script setup lang="ts">
import { ref, watch } from "vue";
import IconCopy from "./icons/IconCopy.vue";

const props = defineProps<{
  password: string;
}>();

const copied = ref(false);

watch(copied, (newVal) => {
  if (newVal) {
    setTimeout(() => {
      copied.value = false;
    }, 2000);
  }
});

function copyPasswordToClipboard() {
  navigator.clipboard.writeText(props.password);
  copied.value = true;
}
</script>

<template>
  <div class="wrapper">
    <h1>{{ password }}</h1>
    <button @click="copyPasswordToClipboard">
      <span v-if="copied">Copied</span>
      <IconCopy />
    </button>
  </div>
</template>

<style scoped>
.wrapper {
  background-color: var(--color-foreground);
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  height: 5rem;
  padding-block: 0;
}

.wrapper button {
  transition: color 200ms ease-in-out;
  text-transform: uppercase;
  display: flex;
  gap: 1rem;
}
.wrapper button:where(:hover, :focus) {
  color: var(--color-strong);
}
</style>
