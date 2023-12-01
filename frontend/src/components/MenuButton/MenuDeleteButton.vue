<script setup>
import { defineProps, defineEmits } from 'vue';
import axios from 'axios';

const props = defineProps(['contentId']);
const emit = defineEmits(['getContentsList']);
const deleteContent = () => {
  axios
    .delete(`http://localhost:3000/content/${props.contentId}`, {
    })
    .then(() => {
      emit("getContentsList");

    })
    .catch((err) => {
      console.log(err);

    });
}
</script>

<template>
  <button class="delete__button" @click="deleteContent">
    <img alt="delete button" src="@/assets/img/icon/delete.svg">
  </button>
</template>


<style lang="scss" scope>
.delete__button {
  background-color: initial;
  margin-left: 10px;
}
</style>