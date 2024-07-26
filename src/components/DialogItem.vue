<template>
  <Transition>
    <div
      v-if="visible"
      :class="['dialog', { overlay }]"
      @click="props.overlayClose ? (visible = false) : void 0"
    >
      <div class="dialog-content" @click.stop>
        <slot></slot>
      </div>
    </div>
  </Transition>
</template>

<script lang="ts" setup>
import { onUnmounted, ref, watch } from 'vue'

interface Props {
  noScroll?: boolean // 禁止滚动条出现
  overlay?: boolean // 是否显示遮罩
  overlayClose?: boolean // 点击遮罩关闭
}
const props = withDefaults(defineProps<Props>(), {
  noScroll: true,
  overlay: true,
  overlayClose: true
})

const dialogVisible = ref(false)
const visible = defineModel<boolean>('visible', {
  required: true,
  default: false
})

watch(
  () => visible.value,
  (newVal: boolean) => {
    if (props.noScroll) toggleBodyScroll(newVal)
    // dialogVisible.value = newVal
  }
)

const toggleBodyScroll = (noScroll: boolean) => {
  if (noScroll) {
    document.documentElement.style.overflow = 'hidden'
  } else {
    document.documentElement.style.overflow = ''
  }
}

onUnmounted(() => {
  if (props.noScroll) toggleBodyScroll(false)
})
</script>

<style scoped>
.dialog {
  position: fixed;
  z-index: 9999;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.dialog.overlay {
  background: rgba(0, 0, 0, 0.5);
}

.dialog-content {
  background: white;
  padding: 20px;
  border-radius: 5px;
  position: relative;
}

.v-enter-active,
.v-leave-active {
  transition: opacity 0.5s ease;
}

.v-enter-from,
.v-leave-to {
  opacity: 0;
}
</style>
