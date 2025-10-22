<template>
  <div class="layout-header">
    <div class="header-midden">
      <div class="cn">电厂数字孪生服务平台</div>
      <div class="en">Power plant digital twin service platform</div>
    </div>
    <div class="header-left">
      <div class="brand-logo">Jennie</div>
      <div
        class="message"
        content="Jennie 数字孪生解决方案 | 基于Three.js打造的电厂智能监控平台，实现设备状态实时可视化、数据智能分析与预警服务"
      ></div>
    </div>
    <div class="header-right">
      <span>{{ currentTime }}</span>
      <span>{{ currentDate }}</span>
      <span>{{ currentWeek }}</span>
      <span>{{ currentWeather }}</span>
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const currentTime = ref('')
const currentDate = ref('')
const currentWeek = ref('')
const currentWeather = ref('13°C')

let timer: number | null = null

const weekDays = [
  '星期日',
  '星期一',
  '星期二',
  '星期三',
  '星期四',
  '星期五',
  '星期六',
]

const updateDateTime = () => {
  const now = new Date()

  // 格式化时间 HH:MM:SS
  const hours = String(now.getHours()).padStart(2, '0')
  const minutes = String(now.getMinutes()).padStart(2, '0')
  const seconds = String(now.getSeconds()).padStart(2, '0')
  currentTime.value = `${hours}:${minutes}:${seconds}`

  // 格式化日期 YYYY-MM-DD
  const year = now.getFullYear()
  const month = String(now.getMonth() + 1).padStart(2, '0')
  const day = String(now.getDate()).padStart(2, '0')
  currentDate.value = `${year}-${month}-${day}`

  // 星期
  currentWeek.value = weekDays[now.getDay()]
}

onMounted(() => {
  updateDateTime()
  timer = window.setInterval(updateDateTime, 1000)
})

onUnmounted(() => {
  if (timer) {
    clearInterval(timer)
  }
})
</script>
<style lang="scss" scoped>
@mixin font-color() {
  background: linear-gradient(0deg, #b9cfff 0%, #fff 99%);
  background-clip: text;
  -webkit-text-fill-color: transparent;
}
@keyframes text-roll {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-100%);
  }
}
@keyframes light-go {
  from {
    left: 500px;
  }
  to {
    left: 1100px;
    opacity: 0;
  }
}
.layout-header {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 80px;
  background-image: url(@/assets/title_bg.png);
  background-repeat: no-repeat;
  background-position: center top;
  background-size: 100% 100%;
  &::after {
    position: absolute;
    bottom: -55px;
    left: 500px;
    width: 100%;
    width: 500px;
    height: 100px;
    content: '';
    background-image: url(@/assets/light_bg.png);
    background-repeat: no-repeat;
    background-size: contain;
    animation: light-go 3s ease-in-out infinite forwards;
  }
  .header-midden {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 100%;
    overflow-x: hidden;
    font-family: DouYu;
    color: #fff;
    .cn {
      font-size: 30px;
      @include font-color;
    }
    .en {
      position: relative;
      font-size: 10px;
      @include font-color;
    }
  }
  .header-left {
    position: absolute;
    top: 20px;
    left: 30px;
    display: flex;
    grid-gap: 10px;
    align-items: center;
    font-size: 18px;
    color: #fff;
    .brand-logo {
      font-family: Furore, Arial, sans-serif;
      font-size: 28px;
      font-weight: bold;
      text-shadow: 0 0 20px rgba(0, 217, 255, 50%);
      text-transform: lowercase;
      letter-spacing: 2px;
      background: linear-gradient(
        135deg,
        #00d9ff 0%,
        #0084ff 50%,
        #00d9ff 100%
      );
      filter: drop-shadow(0 0 10px rgba(0, 217, 255, 30%));
      background-clip: text;
      animation: brand-glow 3s ease-in-out infinite alternate;
      -webkit-text-fill-color: transparent;
    }
    .message {
      display: flex;
      width: 360px;
      overflow: hidden;
      font-size: 14px;
      &::after {
        width: auto;
        text-wrap: nowrap;
        content: attr(content);
        animation: text-roll 25s linear infinite;
        @include font-color;
      }
    }
  }
  @keyframes brand-glow {
    0% {
      filter: drop-shadow(0 0 10px rgba(0, 217, 255, 30%));
    }
    100% {
      filter: drop-shadow(0 0 20px rgba(0, 217, 255, 60%));
    }
  }
  .header-right {
    position: absolute;
    top: 20px;
    right: 30px;
    display: flex;
    grid-gap: 20px;
    font-size: 16px;
    color: #fff;
    span {
      position: relative;
      display: flex;
      align-items: center;
      text-shadow: 0 3px 2px #84a8f663;
      @include font-color;
      &:not(:last-child)::after {
        position: absolute;
        right: -10px;
        width: 2px;
        height: 10px;
        content: '';
        background-color: #fff;
        opacity: 0.2;
      }
    }
  }
}
</style>
