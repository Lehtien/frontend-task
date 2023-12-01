<script setup>
import { defineProps, defineEmits } from "vue";
import MenuDoneButton from './MenuDoneButton.vue';
import MenuNewPageButton from './MenuNewPageButton.vue';

const props = defineProps(['editMode']);

const emit = defineEmits(['getContentsList', 'modeChange']);
const getContentsList = () =>{
  emit("getContentsList");
}

</script>

<template>
  <div>
    <button class="edit__button" v-show="!props.editMode" @click="emit('modeChange')">
      <img alt="edit button" src="@/assets/img/icon/edit.svg">
      <p>Edit</p>
    </button>
    <div class="button__group" v-show="props.editMode">
      <MenuNewPageButton @getContentsList="getContentsList"/>
      <MenuDoneButton  @click="emit('modeChange')" />
    </div>
  </div>
</template>

<style lang="scss" scope>
button {
  height: 40px;
  min-width: 40px;
  background-color: #4CB3F8;
  color: white;
  border-radius: 4px;
  border: none;
  cursor: pointer;

  p {
    margin: 0 auto;
    font-size: 10px;
  }

  &:hover {
    background-color: #3C8EC4;
  }

  &:active {
    background-color: #347CAB;
  }

  &:disabled {
    background-color: #4CB3F8;
  }
}

.edit__button {
  width: 90px;
}

.button__group {
  min-width: 90px;
  display: flex;
  justify-content: space-between;
}
</style>