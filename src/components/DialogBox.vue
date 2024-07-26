<template>
  <DialogItem v-model:visible="visible">
    <p>这是弹窗内容</p>
    <input type="text" />
    <button @click="visible = false">关闭弹窗</button>
  </DialogItem>
</template>

<script lang="ts" setup>
import DialogItem from '@/components/DialogItem.vue'

const visible = defineModel<boolean>('visible', {
  required: true,
  default: false
})
</script>

<style scoped></style>
