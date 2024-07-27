<template>

  <div>
    <h1>Mention Box</h1>
    <div contenteditable="true" ref="contentRef" id="contentRef" @keyup="onUserInput"></div>
    <div class="users-modal" v-if="isModalOpen">
      <div class="user" v-for="i in 5" :key="i">
        <p>User {{ i + 1 }}</p>
      </div>
    </div>
  </div>

</template>

<script lang="ts" setup>
import {ref} from 'vue';

const isModalOpen = ref(false);
const contentRef = ref<HTMLDivElement | null>(null);

const onUserInput = () => {
  const content = contentRef?.value!.innerHTML;
  contentRef!.value!.innerHTML = content.replace(/@/, '<span contenteditable="false">Replaced</span> ');

  const element = contentRef?.value;
  const range = document.createRange();
  const selection = window.getSelection();
  range.setStart(element, element.childNodes.length);
  range.collapse(true);
  selection!.removeAllRanges();
  selection!.addRange(range);

};
</script>