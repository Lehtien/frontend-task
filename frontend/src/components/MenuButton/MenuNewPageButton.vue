<script setup>
import { defineEmits } from "vue";
import axios from 'axios';

const emit = defineEmits(['getContentsList']);
const createNewPage = () => {
  
  axios
    .post("http://localhost:3000/content", {
      title: "タイトル",
      body: "コンテンツ"
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
  <button class="new__page__button" @click="createNewPage">
    <img alt="new page button" src="@/assets/img/icon/+.svg">
    <p>New Page</p>
  </button>
</template>


<style lang="scss" scope>
.new__page__button {
  width: 90px;
  background-color: #FFFFFF;
  border: 2px solid #4CB3F8;
  color: #4CB3F8;

  * {
    transform: translateY(-2px);
  }
}
</style>