<template>
  <div class="label" @click="onClick">{{ displayName }}</div>
</template>
<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'

interface PropsType {
  name: string
  translationKey?: string
  index?: number
}
const props = defineProps<PropsType>()
const { t } = useI18n()

const displayName = computed(() => {
  if (props.translationKey && props.index !== undefined) {
    return `${props.index}# ${t(props.translationKey)}`
  }
  return props.name
})

const onClick = () => {
  alert(displayName.value)
}
</script>
<style lang="scss" scoped>
.label {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 135px;
  height: 40px;
  font-weight: bolder;
  color: #fff;
  pointer-events: all;
  cursor: pointer;
  background-image: url(@/assets/label_bg.png);
  background-repeat: no-repeat;
  background-size: 100% 100%;
}
</style>
