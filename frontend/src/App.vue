<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';
import SiteLogo from './components/SiteLogo.vue';
import MenuList from './components/MenuList.vue';
import MainContent from '@/components/MainContent.vue';

const content = ref(null);
const getContent = (contentId) => {
  axios
    .get(`http://localhost:3000/content/${contentId}`)
    .then((res) => {
      content.value = res.data;
    })
    .catch((err) => {
      console.log(err);
    });
}

const menuList = ref();
const getContentsList = () => {
  menuList.value.getContentsList();
}
onMounted(() => {
  let initContentsList = [];
  axios
    .get("http://localhost:3000/content")
    .then((res) => {
      initContentsList = res.data;
      if (initContentsList.length > 0) {
        content.value = initContentsList[0];

      }
    })
    .catch((err) => {
      console.log(err);
    });
});
</script>

<template>
  <div class="site">
    <div class="sub">
      <SiteLogo />
      <MenuList @getContent="getContent" ref="menuList" />
    </div>
    <MainContent :content="content" @getContentsList="getContentsList" @getContent="getContent(content.id)"/>
  </div>
</template>

<style lang="scss" scope>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap');
#app {
  font-family: 'Noto Sans JP', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #333333;
  background-color: #FFFFFF;
}

body {
  margin: 0;
  font-size: 16px;
}

.site {
  display: flex;
}

.sub {
  border-right: 1px solid #F6F8FA;
  width: 280px;
}

.title__font__size {
  font-size: 24px;
}

.caption__font__size {
  font-size: 12px;
}

.minimun__font__size {
  font-size: 10px;
}

input:focus,
textarea:focus {
  outline: solid 2px #4CB3F8;
}
</style>
