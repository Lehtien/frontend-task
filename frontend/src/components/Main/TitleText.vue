<script setup>
import { ref, defineProps, defineEmits, nextTick, watchEffect } from 'vue';
import EditButton from '@/components/Button/EditButton.vue';

const emit = defineEmits(['getContentsList', 'cancel']);

const props = defineProps(['content']);

const title = ref(props.content?.title);
watchEffect(() => {
  title.value = props.content?.title;
});
const updateTitle = (event) => {
  title.value = event.target.value;
}

const disabled = ref(true);
const toggleDisabled = () => {
  if (disabled.value === true) {
    disabled.value = null;
    nextTick(() => {
      document.getElementById("title_text").focus();
    })
  } else {
    disabled.value = true;
  }
}
</script>

<template>
  <div class="title">
    <input id="title_text" class="title__font__size title__text" :disabled=disabled :value=title @input="updateTitle" />
    <div class="button">
      <EditButton @toggleDisabled=toggleDisabled @getContentsList="emit('getContentsList')" @cancel="emit('cancel')"
        :contentId="props.content?.id" :title="title" />
    </div>
  </div>
</template>

<style lang="scss" scope>
.title {
  display: flex;

  .title__text {
    margin: 0px 30px 20px;
    width: 100%;
    background-color: #F5F8FA;
    border: 0;
    border-radius: 8px;
    color: #333333;
    font-family: NotoSansJP-Bold;
    font-weight: 700;

  }
}
</style>
