<script setup>
import { ref, defineEmits, defineExpose } from 'vue';
import MenuEditButton from '@/components/MenuButton/MenuEditButton.vue';
import MenuDeleteButton from '@/components/MenuButton/MenuDeleteButton.vue';
import axios from 'axios';

const contentsList = ref([]);
const getContentsList = () => {
  axios
    .get("http://localhost:3000/content")
    .then((res) => {
      contentsList.value = res.data;
    })
    .catch((err) => {
      console.log(err);
    });
}

getContentsList();

defineExpose({
  getContentsList,
});

const emit = defineEmits(['getContent']);
const sendContentId = (contentId) => {
  for(let content of contentsList.value) {
    document.getElementById(`title${content.id}`).classList.remove("active");
  }
  document.getElementById(`title${contentId}`).classList.add("active");
  emit("getContent", contentId);
}

const editMode = ref(false);
const modeChange = () => {
  editMode.value = !editMode.value;
}
</script>

<template>
  <div class="menu">
    <div class="title__list">
      <div v-for="(item, index) in contentsList" :key="index" :id="'title' + item.id" class="title__group">
        <span class="title" @click="sendContentId(item.id)">{{ item.title }}</span>
        <MenuDeleteButton :contentId=item.id @getContentsList="getContentsList" v-show="editMode" @modeChange="modeChange" />
      </div>
    </div>
    <div class="button">
      <MenuEditButton @getContentsList="getContentsList" :editMode="editMode"  @modeChange="modeChange"/>
    </div>
  </div>
</template>


<style lang="scss" scope>
.menu {
  align-content: space-between;
  text-align: left;

  .title__list {
    height: 100vh;
    margin-left: 40px;
    margin-right: 10px;
    overflow: auto;

    .title__group {
      cursor: pointer;
      height: 44px;
      line-height: 44px;
      display: flex;
      justify-content: space-between;
      overflow: hidden;

      .title {
        width: 100%;
        padding-left: 10px;
        font-family: NotoSansJP-Regular;
      }
      &.active {
        background-color: #F5F8FA;
        border-radius: 4px;
        color: #32A8F8;
        .title {
          font-weight: 700;
        }
      }
    }
  }

  .button {
    background-color: #F6F8FA;
    text-align: right;
    width: 100%;
    height: 60px;

    button {
      margin: 1em;
    }
  }

}
</style>