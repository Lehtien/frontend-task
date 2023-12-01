<script setup>
import { ref, defineProps, defineEmits } from "vue";
import SaveButton from "./SaveButton.vue";
import CancelButton from "./CancelButton.vue";

const props = defineProps(['contentId', 'title', 'body']);

const editMode = ref(false);

const emit = defineEmits(['toggleDisabled', 'getContentsList', 'cancel']);
const modeChange = () => {
  editMode.value = !editMode.value;
  emit("toggleDisabled");
}
const cancel = () => {
  modeChange();
  emit('cancel');

}
</script>

<template>
  <div>
    <button class="edit__button" v-show="!editMode" @click="modeChange">
      <img alt="edit button" src="@/assets/img/icon/edit.svg">
      <p>Edit</p>
    </button>
    <div class="button__group" v-show="editMode">
      <CancelButton @cancel="cancel" />
      <SaveButton :contentId="props.contentId" :title="props.title" :body="props.body"
        @getContentsList="emit('getContentsList')" @click="modeChange" />
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