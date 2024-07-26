<template>
  <div>
    <div><button @click="visible = true">弹出</button></div>
    <div>
      <DialogBox v-model:visible="visible" />
    </div>
  </div>
</template>

<script setup lang="ts">
import DialogBox from '@/components/DialogBox.vue'
import { ref } from 'vue'

const visible = ref(false)
</script>

<style scoped></style>
