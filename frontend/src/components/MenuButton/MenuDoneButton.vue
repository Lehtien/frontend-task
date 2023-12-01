<script setup>
import { defineEmits } from 'vue';
const emit = defineEmits(['modeChange']);
</script>

<template>
  <button class="done__button"  @click="emit('modeChange')">
    <img alt="done button" src="@/assets/img/icon/done.svg">
    <p>Done</p>
  </button>
</template>


<style lang="scss" scope>

.done__button {
  width: 90px;
}
</style>