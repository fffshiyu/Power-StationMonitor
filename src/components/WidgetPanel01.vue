<template>
  <LayoutPanel :title="t('panels.faultComparison')">
    <div class="container" ref="container"></div>
  </LayoutPanel>
</template>
<script setup lang="ts">
import LayoutPanel from './LayoutPanel.vue'
import { nextTick, onMounted, watch } from 'vue'
import useEcharts from '@/hooks/useEcharts'
import { useI18n } from 'vue-i18n'

const { t, locale } = useI18n()

const { container, echarts, setOption } = useEcharts()

const updateChart = () => {
  const options = generateOptions()
  setOption(options)
}

const generateOptions = () => {
  return {
    legend: {
      show: true,
      right: 0,
      textStyle: {
        color: '#fff',
      },
    },
    tooltip: {
      trigger: 'axis',
      backgroundColor: '#000',
      borderColor: '#333',
      textStyle: {
        color: '#fff',
      },
    },
    grid: {
      left: '4%',
      right: '4%',
      bottom: '0%',
      top: '20%',
      containLabel: true,
    },
    xAxis: {
      type: 'category',
      axisLine: {
        show: false,
      },
      axisTick: {
        show: false,
      },
      axisLabel: {
        color: '#fff',
        margin: 10,
      },
      data: [t('chart.months.aug'), t('chart.months.sep'), t('chart.months.oct'), t('chart.months.nov'), t('chart.months.dec')],
    },
    yAxis: {
      type: 'value',
      axisLabel: {
        color: '#fff',
      },
      splitLine: {
        lineStyle: {
          color: '#c8c8c830',
          type: 'dashed',
        },
      },
    },
    series: [
      {
        name: t('chart.year2024'),
        type: 'bar',
        emphasis: { focus: 'series' },
        data: [320, 332, 301, 334, 390],
        barWidth: 20,
        barGap: '20%',
        itemStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            { offset: 0, color: 'rgba(0, 254, 169, 1)' },
            { offset: 1, color: 'rgba(0, 254, 169, 0.1)' },
          ]),
        },
      },
      {
        name: t('chart.year2025'),
        type: 'bar',
        emphasis: { focus: 'series' },
        data: [220, 182, 191, 234, 290],
        barWidth: 20,
        barGap: '20%',
        itemStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            { offset: 0, color: 'rgba(87, 153, 214, 1)' },
            { offset: 1, color: 'rgba(87, 153, 214, 0.1)' },
          ]),
        },
      },
    ],
  }
}

onMounted(() => {
  nextTick(() => {
    updateChart()
  })
})

watch(locale, () => {
  nextTick(() => {
    updateChart()
  })
})
</script>

<style lang="scss" scoped>
.container {
  height: 100%;
}
</style>
