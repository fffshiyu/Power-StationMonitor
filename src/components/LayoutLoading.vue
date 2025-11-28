<template>
  <div class="layout-loading" v-show="loading.isLoading">
    <div class="loading-gif"></div>
    <div class="loading-tip">
      {{ t('loading.text') }} ({{ loading.loaded }}/{{ loading.total }}) ...
    </div>
  </div>
</template>
<script setup lang="ts">
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

interface PropsType {
  loading: {
    total: number // 全部
    loaded: number // 已加载
    isLoading: boolean // 执行状态
  }
}
const props = defineProps<PropsType>()
</script>
<style lang="scss" scoped>
.layout-loading {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 99999;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  background: #000;
  .loading-gif {
    width: 1000px;
    height: 250px;
    background-image: url('@/assets/loading.gif');
    background-repeat: no-repeat;
    background-size: 100% 100%;
  }
  .loading-tip {
    // font-family: Douyu;

    // font-style: italic;
    // font-weight: bolder;
    color: #5fb9c7;
  }
}
</style>
