<script setup>
import { defineProps, defineEmits } from 'vue';
import axios from 'axios';

const props = defineProps(['contentId', 'title', 'body']);
const emit = defineEmits(['getContentsList']);

const updateContent = () => {
  axios
    .put(`http://localhost:3000/content/${props.contentId}`, {
      title: props.title,
      body: props.body
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
  <button class="save__button" @click="updateContent">
    <img alt="save button" src="@/assets/img/icon/save.svg">
    <p>Save</p>
  </button>
</template>