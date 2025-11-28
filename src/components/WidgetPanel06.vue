<template>
  <LayoutPanel :title="t('panels.warningStatus')">
    <div class="wrap">
      <div class="item-list" ref="container">
        <div
          class="item"
          v-for="{ name, event, type, time } in list"
          :style="{ background: generateTypeColor(type, '55') }"
        >
          <div
            class="item-circle"
            :style="{ background: generateTypeColor(type) }"
          ></div>

          <div class="item-name">{{ name }}</div>
          <div class="item-type">{{ t(event) }}</div>
          <div class="item-time">{{ time }}</div>
        </div>
      </div>
    </div>
  </LayoutPanel>
</template>
<script setup lang="ts">
import LayoutPanel from './LayoutPanel.vue'
import { ref, onMounted } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()

const list = ref<any[]>([
  {
    name: '1# Transformer Sensor',
    event: 'warning.disconnected',
    type: 1,
    time: '08:21',
  },
  {
    name: '23# Temp/Humidity Sensor',
    event: 'warning.smokeValue',
    type: 3,
    time: '08:32',
  },
  {
    name: '9# Infrared Detector',
    event: 'warning.disconnected',
    type: 2,
    time: '09:44',
  },
  {
    name: '2# Fan Room',
    event: 'warning.waterDetected',
    type: 3,
    time: '12:53',
  },
  {
    name: '18# Patrol Anchor',
    event: 'warning.disconnected',
    type: 3,
    time: '14:15',
  },
  {
    name: '7# Patrol Anchor',
    event: 'warning.disconnected',
    type: 2,
    time: '14:45',
  },
  {
    name: '26# Infrared Detector',
    event: 'warning.abnormalDetected',
    type: 2,
    time: '14:59',
  },
  {
    name: '3# Fan Room',
    event: 'warning.fanStuck',
    type: 1,
    time: '16:42',
  },
  {
    name: '6# Transformer Sensor',
    event: 'warning.disconnected',
    type: 2,
    time: '17:43',
  },
  {
    name: '1# Transformer Sensor',
    event: 'warning.disconnected',
    type: 1,
    time: '08:21',
  },
  {
    name: '23# Temp/Humidity Sensor',
    event: 'warning.smokeValue',
    type: 3,
    time: '08:32',
  },
  {
    name: '9# Infrared Detector',
    event: 'warning.disconnected',
    type: 2,
    time: '09:44',
  },
  {
    name: '2# Fan Room',
    event: 'warning.waterDetected',
    type: 3,
    time: '12:53',
  },
  {
    name: '18# Patrol Anchor',
    event: 'warning.disconnected',
    type: 3,
    time: '14:15',
  },
  {
    name: '7# Patrol Anchor',
    event: 'warning.disconnected',
    type: 2,
    time: '14:45',
  },
  {
    name: '26# Infrared Detector',
    event: 'warning.abnormalDetected',
    type: 2,
    time: '14:59',
  },
  {
    name: '7# Patrol Anchor',
    event: 'warning.disconnected',
    type: 2,
    time: '14:45',
  },
  {
    name: '26# Infrared Detector',
    event: 'warning.abnormalDetected',
    type: 2,
    time: '14:59',
  },
  {
    name: '7# Patrol Anchor',
    event: 'warning.disconnected',
    type: 2,
    time: '14:45',
  },
  {
    name: '26# Infrared Detector',
    event: 'warning.abnormalDetected',
    type: 2,
    time: '14:59',
  },
  {
    name: '7# Patrol Anchor',
    event: 'warning.disconnected',
    type: 2,
    time: '14:45',
  },
  {
    name: '26# Infrared Detector',
    event: 'warning.abnormalDetected',
    type: 2,
    time: '14:59',
  },
  {
    name: '7# Patrol Anchor',
    event: 'warning.disconnected',
    type: 2,
    time: '14:45',
  },
  {
    name: '26# Infrared Detector',
    event: 'warning.abnormalDetected',
    type: 2,
    time: '14:59',
  },
])

const container = ref()

const generateTypeColor = (type: 1 | 2 | 3, gradual = false) => {
  const colors = {
    1: '#74fabd',
    2: '#5bc7fa',
    3: '#f1bd49',
  }
  if (gradual) {
    return `linear-gradient(90deg, ${colors[type]}77 , transparent )`
  } else {
    return colors[type]
  }
}

let timer: any
onMounted(() => {
  if (timer) window.clearInterval(timer)
  timer = setInterval(() => {
    container.value.classList.add('scroll')
    setTimeout(() => {
      if (!timer) return void 0
      container.value.classList.remove('scroll')
      list.value.push(list.value.shift())
    }, 2000)
  }, 3000)
})
</script>

<style lang="scss" scoped>
@keyframes row-out {
  from {
    top: 0;
  }
  to {
    top: -36px;
  }
}
.wrap {
  height: 100%;
  overflow: hidden;
}
.item-list {
  display: flex;
  flex-direction: column;
  grid-gap: 8px;
  height: 670px;

  // overflow: hidden;
  &.scroll {
    position: relative;
    animation: row-out 1s linear forwards;
    .row:first-child {
      opacity: 0;
      transition: opacity 1s;
    }
  }
  .item {
    position: relative;
    display: flex;
    align-items: center;
    padding: 5px;
    font-size: 16px;
    .item-circle {
      position: absolute;
      left: 10px;
      width: 5px;
      height: 10px;
    }
    .item-name {
      width: 50%;
      padding-left: 15px;
    }
    .item-type {
      width: 30%;
    }
    .item-time {
      width: 20%;
      text-align: end;
    }
  }
}
</style>
