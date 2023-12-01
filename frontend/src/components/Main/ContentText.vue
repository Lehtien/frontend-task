<script setup>
import { ref, defineProps, defineEmits, nextTick, watchEffect } from 'vue';
import EditButton from '@/components/Button/EditButton.vue';

const props = defineProps(['content']);
const emit = defineEmits(['cancel']);

const body = ref(props.content?.body);
watchEffect(() => {
  body.value = props.content?.body;
});
const updateBody = (event) => {
  body.value = event.target.value;
}

const disabled = ref(true);
const toggleDisabled = () => {
  if (disabled.value === true) {
    disabled.value = null;
    nextTick(() => {
      document.getElementById("contents_text").focus();
    })
  } else {
    disabled.value = true;
  }
}

</script>
<template>
  <div class="contents">
    <textarea id="contents_text" class="contents_text" :disabled=disabled :value="body" @input="updateBody" />
    <div class="button">
      <EditButton @toggleDisabled=toggleDisabled :contentId="props.content?.id" :body="body" @cancel="emit('cancel')" />
    </div>
  </div>
</template>


<style lang="scss" scope>
.contents {
  display: flex;
  height: calc(100vh - 60px);

  .contents_text {
    background-color: #FFFFFF;
    border-radius: 8px;
    padding: 30px;
    width: 100%;
    border: 0;
    resize: none;
    color: #333333;
    font-size: 16px;
    font-family: 'Noto Sans JP', sans-serif;
  }
}
</style>