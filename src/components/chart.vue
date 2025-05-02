<template>
  <div style="position: relative; width: 100%; height: 800px">
    <VChart :option="chartOption" autoresize />
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from 'vue'
import VChart from 'vue-echarts'
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import { GraphChart } from 'echarts/charts'
import { TooltipComponent, LegendComponent, GraphicComponent } from 'echarts/components'

use([CanvasRenderer, GraphChart, TooltipComponent, LegendComponent, GraphicComponent])

const chartRef = ref(null)
const rawData = defineModel('rawData', [])
const rawConnections = defineModel('rawConnections', [])
const chartOption = ref({})
const labelColors = [
  '#ff5722',
  '#3f51b5',
  '#4caf50',
  '#e91e63',
  '#009688',
  '#ff9800',
  '#9c27b0',
  '#795548',
]

function buildForceLayout() {
  const nodes = []
  const links = []
  const funcMap = {}
  const labelMap = {}
  const labelGroups = {}

  rawData.value.forEach((f) => {
    const id = f.func_name
    const label = f.label
    const color = labelColors[label % labelColors.length]

    const node = {
      id,
      name: f.func_name,
      category: label,
      value: f.count,
      symbolSize: Math.max(10, f.count * 3),
      itemStyle: { color },
      draggable: true,
      tooltip: {
        formatter: `
          <b>${f.func_name}</b><br/>
          文件: ${f.file_path}<br/>
          行: ${f.lineno}-${f.end_lineno}<br/>
          时间: ${f.execution_time}ms<br/>
          次数: ${f.count}
        `,
      },
    }

    funcMap[id] = node
    nodes.push(node)
    if (!labelGroups[label]) labelGroups[label] = []
    labelGroups[label].push(node)
    labelMap[label] = true
  })

  rawConnections.value.forEach((c) => {
    const source = c.caller_tuple[1]
    const target = c.called_tuple[1]
    if (funcMap[source] && funcMap[target]) {
      links.push({
        source,
        target,
        lineStyle: {
          width: Math.min(10, c.call_count),
          color: '#00c853',
        },
        tooltip: {
          formatter: `
            <b>${source} -> ${target}</b><br/>
            调用次数: ${c.call_count}<br/>
            执行时间: ${c.execution_time}ms
          `,
        },
      })
    }
  })

  chartOption.value = {
    tooltip: { trigger: 'item' },
    legend: {
      data: Object.keys(labelMap).map((label) => `微服务 ${label}`),
    },
    series: [
      {
        type: 'graph',
        layout: 'force',
        roam: true,
        label: { show: true, position: 'right' },
        force: {
          repulsion: 400,
          edgeLength: 100,
        },
        categories: Object.keys(labelMap).map((label, i) => ({
          name: `微服务 ${label}`,
          itemStyle: { color: labelColors[i % labelColors.length] },
        })),
        data: nodes,
        links: links,
        draggable: true,
        emphasis: {
          focus: 'adjacency',
          lineStyle: { width: 5 },
        },
      },
    ],
    graphic: [], // 初始为空，后面再补
  }

  nextTick(() => {
    const chart = chartRef.value?.getEChartsInstance()
    if (!chart) return

    setTimeout(() => {
      const series = chart.getModel().getSeriesByIndex(0)
      const positions = series.getData()

      const markRects = []

      Object.entries(labelGroups).forEach(([label, group]) => {
        const coords = group
          .map((node) => {
            const idx = positions.indexOfName(node.id)
            const pos = positions.getItemLayout(idx)
            return pos ? { x: pos[0], y: pos[1] } : null
          })
          .filter(Boolean)

        console.log('okokok')

        if (coords.length === 0) return

        const minX = Math.min(...coords.map((c) => c.x))
        const minY = Math.min(...coords.map((c) => c.y))
        const maxX = Math.max(...coords.map((c) => c.x))
        const maxY = Math.max(...coords.map((c) => c.y))

        console.log('okokokok')
        markRects.push({
          type: 'group',
          children: [
            {
              type: 'rect',
              shape: {
                x: minX - 50,
                y: minY - 50,
                width: maxX - minX + 100,
                height: maxY - minY + 100,
              },
              style: {
                stroke: labelColors[label % labelColors.length],
                lineWidth: 2,
                fill: labelColors[label % labelColors.length] + '20', // 透明背景
                lineDash: [5, 5],
              },
              z: -1,
            },
            {
              type: 'text',
              style: {
                text: `微服务 ${label}`,
                fill: labelColors[label % labelColors.length],
                font: 'bold 14px sans-serif',
              },
              left: minX - 45,
              top: minY - 65,
              z: -1,
            },
          ],
        })
      })

      chart.setOption({
        graphic: markRects,
      })
    }, 800) // 需要等待 force 布局稳定（延迟）
  })
}

watch([rawData, rawConnections], buildForceLayout, { immediate: true })
</script>
