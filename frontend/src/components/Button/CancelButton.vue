<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['modeChange', 'cancel']);
const cancel = () => {
  emit("modeChange");
  emit("cancel")
}

</script>

<template>
  <button class="cancel__button" @click=cancel>
    <img alt="cancel button" src="@/assets/img/icon/cancel.svg">
    <p>Cancel</p>
  </button>
</template>