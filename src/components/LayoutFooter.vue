<template>
  <div class="layout-footer">
    <div class="item" :style="warmingStyle" @click="warmingHandle">
      {{ state.isWarming ? t('footer.cancelWarning') : t('footer.equipmentWarning') }}
    </div>
    <div class="item" :style="inspectStyle" @click="inspectHandle">
      {{ state.isInspect ? t('footer.cancelInspection') : t('footer.roamingInspection') }}
    </div>
  </div>
</template>
<script setup lang="ts">
import { reactive, computed, inject } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const state = reactive({
  isWarming: false,
  isInspect: false,
})

const events = inject<any>('events')

const warmingHandle = async () => {
  if (state.isInspect) return void 0
  state.isWarming = !state.isWarming
  if (state.isWarming) {
    events.startWarming()
  } else {
    events.stopWarming()
  }
  // state.isWarming = !state.isWarming
  // await events.startInspect()
}

const inspectHandle = async () => {
  if (state.isWarming) return void 0
  state.isInspect = !state.isInspect
  if (state.isInspect) {
    await events.startInspect()
    state.isInspect = false
  } else {
    await events.stopInspect()
  }
}

const warmingStyle = computed(() => {
  const style: any = {}
  if (state.isInspect) {
    style.cursor = 'not-allowed'
  } else {
    style.cursor = 'pointer'
  }

  if (state.isWarming) {
    style.color = '#5bc7fa'
  } else {
    style.color = '#fff'
  }
  return style
})

const inspectStyle = computed(() => {
  const style: any = {}
  if (state.isWarming) {
    style.cursor = 'not-allowed'
  } else {
    style.cursor = 'pointer'
  }

  if (state.isInspect) {
    style.color = '#5bc7fa'
  } else {
    style.color = '#fff'
  }
  return style
})
</script>
<style lang="scss" scoped>
.layout-footer {
  position: absolute;
  bottom: 0;
  left: 0;
  z-index: 999;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100px;
  background-image: url('@/assets/footer_bg.png');
  background-repeat: no-repeat;
  background-size: 100% 100%;
  .item {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 170px;
    height: 50px;
    padding: 0 10px;
    overflow: hidden;
    font-family: Douyu;
    font-size: 14px;
    color: #fff;
    text-overflow: ellipsis;
    white-space: nowrap;
    cursor: pointer;
    background-image: url('@/assets/footer_item_bg.png');
    background-repeat: no-repeat;
    background-size: 100% 100%;
  }
}
</style>
