<template>
  <LayoutPanel :title="t('panels.equipmentScale')">
    <div class="weather-monitor">
      <div
        v-for="(item, index) in source"
        :key="index"
        class="widget-weather-item"
      >
        <div class="weather-icon" :class="item.icon"></div>
        <div class="weather-label">{{ t(item.label) }}</div>
        <div class="weather-value">
          <span class="value">{{ item.value }}</span>
          <span class="unit">{{ t(item.unit) }}</span>
        </div>
      </div>
    </div>
  </LayoutPanel>
</template>
<script setup lang="ts">
import LayoutPanel from './LayoutPanel.vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const source = [
  {
    icon: 'fa-solid fa-temperature-three-quarters',
    label: 'equipment.glassDetector',
    value: '23',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-shower',
    label: 'equipment.fanRoom',
    value: '23',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-fan',
    label: 'equipment.groundingTransformer',
    value: '23',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-signs-post',
    label: 'equipment.patrolAnchor',
    value: '11',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-wind',
    label: 'equipment.highVoltageDetector',
    value: '63',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-cloud-rain',
    label: 'equipment.infraredDetector',
    value: '23',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-whiskey-glass',
    label: 'equipment.switchCabinet',
    value: '12',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-water',
    label: 'equipment.smokeDetector',
    value: '12',
    unit: 'equipment.unit',
  },
  {
    icon: 'fa-solid fa-fill-drip',
    label: 'equipment.waterDetector',
    value: '13.2',
    unit: 'equipment.unit',
  },
]
</script>

<style lang="scss" scoped>
.container {
  height: 100%;

  //   background-color: red;
}
.weather-monitor {
  box-sizing: border-box;
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
  height: 100%;
  padding-top: 10px;

  $icon-size: 34px;
  .widget-weather-item {
    box-sizing: border-box;
    display: flex;
    display: grid;
    grid-template-rows: repeat(2, 1fr);
    grid-template-columns: $icon-size auto;
    grid-column-gap: 10px;
    align-items: center;
    width: 100%;
    height: 100%;
    padding: 0 8px;
    background-color: rgba(93, 101, 122, 16%);
    .weather-icon {
      display: flex;
      grid-row: 1 /3;
      align-items: center;
      justify-content: center;
      width: $icon-size;
      height: $icon-size;
      border: 1px solid #5bc7fa;
      border-radius: 50%;

      // box-shadow: 0 0 10px #75fbb87d;
    }
    .weather-label {
      margin-top: 10px;
      overflow: hidden;
      font-size: 11px;
      color: #999;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    .weather-value {
      margin-bottom: 6px;
      font-size: 14px;
    }
  }
}
</style>
