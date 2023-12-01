<script setup>
import { defineProps, defineEmits } from 'vue';
import TitleText from './Main/TitleText.vue';
import ContentText from './Main/ContentText.vue';

const props = defineProps(['content']);
const emit = defineEmits(['getContentsList', 'getContent']);

</script>

<template>
  <div class="main__wrapper">
    <div class="main">
      <TitleText :content=props.content @getContentsList="emit('getContentsList')" @cancel="emit('getContent')"/>
      <ContentText :content="props.content" @cancel="emit('getContent')"/>
    </div>
    <div class="copyright caption__font__size">
      <span>Copyright ©2021 Sample</span>
      <span>運営会社</span>
    </div>
  </div>
</template>

<style lang="scss" scope>
.main__wrapper {
  width: 100%;
}

.main {
  background-color: #F5F8FA;
  border-radius: 16px;
  margin: 30px 40px 0 40px;
  padding: 30px;
  text-align: left;

  .button {
    margin-left: 20px;
  }
}

.copyright {
  display: flex;
  justify-content: space-between;
  height: 60px;
  line-height: 60px;
  text-align: left;
  padding: 0 40px;
}
</style>