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
  if (!props.password) return
  navigator.clipboard.writeText(props.password);
  copied.value = true;
}
</script>

<template>
  <div class="wrapper">
    <h1 v-if="password">{{ password }}</h1>
    <h1 v-else class="o-25">P4$5W0rD!</h1>
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
  gap: 0.5rem;
  align-items: center;
  height: 5rem;
  padding-block: 0;
}

.wrapper h1 {
  flex-grow: 1;
  overflow-x: hidden;
  white-space: nowrap;
}

.wrapper button {
  transition: color 200ms ease-in-out;
  text-transform: uppercase;
  flex-shrink: 0;
  display: flex;
  gap: 1rem;
  color: var(--color-strong);
  border: 2px solid
}
.wrapper button:hover {
  color: var(--color-text);
}

.o-25 {
  opacity: 0.25;
  user-select: none;
}
</style>
