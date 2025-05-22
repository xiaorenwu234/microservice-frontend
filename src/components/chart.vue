<template>
  <v-chart :option="chartOption" autoresize style="width: 7000px; height: 5000px" />
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import VChart from 'vue-echarts'
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import { ScatterChart } from 'echarts/charts'
import { TitleComponent, TooltipComponent, GraphicComponent } from 'echarts/components'

use([CanvasRenderer, ScatterChart, TitleComponent, TooltipComponent, GraphicComponent])

const rawData = ref([
  {
    "func_name": "com.example.demo.controller.UserController.registerUser(com.example.demo.model.User)",
    "label": "0"
  },
  {
    "func_name": "com.example.demo.service.UserService.getUserByUsername(java.lang.String)",
    "label": "0"
  },
  {
    "func_name": "com.example.demo.controller.UserController.getUserByUsername(java.lang.String)",
    "label": "0"
  },
  {
    "func_name": "com.example.demo.service.UserService.getUserById(java.lang.Long)",
    "label": "0"
  },
  {
    "func_name": "com.example.demo.controller.UserController.getUserById(java.lang.Long)",
    "label": "0"
  },
  {
    "func_name": "com.example.demo.service.UserService.registerUser(com.example.demo.model.User)",
    "label": "0"
  },
  {
    "func_name": "com.example.demo.controller.OrderController.createOrder(com.example.demo.model.Order)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.controller.OrderController.getOrderById(java.lang.Long)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.controller.OrderDetailController.addOrderDetail(com.example.demo.model.OrderDetail)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.service.OrderService.getPaymentRecordByOrderId(java.lang.Long)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.service.OrderDetailService.addOrderDetail(com.example.demo.model.OrderDetail)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.service.OrderService.createOrder(com.example.demo.model.Order)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.service.OrderService.getOrderDetailsByOrderId(java.lang.Long)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.service.OrderService.getOrderById(java.lang.Long)",
    "label": "4"
  },
  {
    "func_name": "com.example.demo.service.CategoryService.addCategory(com.example.demo.model.Category)",
    "label": "2"
  },
  {
    "func_name": "com.example.demo.service.CategoryService.getCategoryByName(java.lang.String)",
    "label": "2"
  },
  {
    "func_name": "com.example.demo.controller.CategoryController.getCategoryByName(java.lang.String)",
    "label": "2"
  },
  {
    "func_name": "com.example.demo.controller.CategoryController.addCategory(com.example.demo.model.Category)",
    "label": "2"
  },
  {
    "func_name": "com.example.demo.controller.ProductController.getProductById(java.lang.Long)",
    "label": "3"
  },
  {
    "func_name": "com.example.demo.service.ProductService.getProductByName(java.lang.String)",
    "label": "3"
  },
  {
    "func_name": "com.example.demo.controller.ProductController.getProductByName(java.lang.String)",
    "label": "3"
  },
  {
    "func_name": "com.example.demo.controller.ProductController.addProduct(com.example.demo.model.Product)",
    "label": "3"
  },
  {
    "func_name": "com.example.demo.service.ProductService.getProductById(java.lang.Long)",
    "label": "3"
  },
  {
    "func_name": "com.example.demo.service.ProductService.addProduct(com.example.demo.model.Product)",
    "label": "3"
  },
  {
    "func_name": "com.example.demo.service.PaymentRecordService.addPaymentRecord(com.example.demo.model.PaymentRecord)",
    "label": "1"
  },
  {
    "func_name": "com.example.demo.controller.PaymentRecordController.addPaymentRecord(com.example.demo.model.PaymentRecord)",
    "label": "1"
  }
])

const rawConnections = ref([
  {
    "caller": "com.example.demo.controller.PaymentRecordController.addPaymentRecord(com.example.demo.model.PaymentRecord)",
    "called": "com.example.demo.service.PaymentRecordService.addPaymentRecord(com.example.demo.model.PaymentRecord)",
    "execution_time": 13,
    "call_count": 2
  },
  {
    "caller": "com.example.demo.controller.OrderDetailController.addOrderDetail(com.example.demo.model.OrderDetail)",
    "called": "com.example.demo.service.OrderDetailService.addOrderDetail(com.example.demo.model.OrderDetail)",
    "execution_time": 35,
    "call_count": 4
  },
  {
    "caller": "com.example.demo.controller.OrderController.getOrderById(java.lang.Long)",
    "called": "com.example.demo.service.OrderService.getOrderById(java.lang.Long)",
    "execution_time": 74,
    "call_count": 2
  },
  {
    "caller": "com.example.demo.service.OrderService.getOrderById(java.lang.Long)",
    "called": "com.example.demo.service.OrderService.getOrderDetailsByOrderId(java.lang.Long)",
    "execution_time": 29,
    "call_count": 2
  },
  {
    "caller": "com.example.demo.service.OrderService.getOrderById(java.lang.Long)",
    "called": "com.example.demo.service.OrderService.getPaymentRecordByOrderId(java.lang.Long)",
    "execution_time": 15,
    "call_count": 2
  },
  {
    "caller": "com.example.demo.controller.OrderController.createOrder(com.example.demo.model.Order)",
    "called": "com.example.demo.service.OrderService.createOrder(com.example.demo.model.Order)",
    "execution_time": 85,
    "call_count": 2
  },
  {
    "caller": "com.example.demo.service.OrderService.createOrder(com.example.demo.model.Order)",
    "called": "com.example.demo.service.UserService.getUserById(java.lang.Long)",
    "execution_time": 11,
    "call_count": 2
  },
  {
    "caller": "com.example.demo.service.OrderService.createOrder(com.example.demo.model.Order)",
    "called": "com.example.demo.service.ProductService.getProductById(java.lang.Long)",
    "execution_time": 17,
    "call_count": 2
  },
  {
    "caller": "com.example.demo.controller.ProductController.getProductById(java.lang.Long)",
    "called": "com.example.demo.service.ProductService.getProductById(java.lang.Long)",
    "execution_time": 88,
    "call_count": 8
  },
  {
    "caller": "com.example.demo.controller.ProductController.getProductByName(java.lang.String)",
    "called": "com.example.demo.service.ProductService.getProductByName(java.lang.String)",
    "execution_time": 166,
    "call_count": 8
  },
  {
    "caller": "com.example.demo.controller.CategoryController.getCategoryByName(java.lang.String)",
    "called": "com.example.demo.service.CategoryService.getCategoryByName(java.lang.String)",
    "execution_time": 87,
    "call_count": 4
  },
  {
    "caller": "com.example.demo.controller.ProductController.addProduct(com.example.demo.model.Product)",
    "called": "com.example.demo.service.ProductService.addProduct(com.example.demo.model.Product)",
    "execution_time": 97,
    "call_count": 10
  },
  {
    "caller": "com.example.demo.controller.CategoryController.addCategory(com.example.demo.model.Category)",
    "called": "com.example.demo.service.CategoryService.addCategory(com.example.demo.model.Category)",
    "execution_time": 64,
    "call_count": 7
  },
  {
    "caller": "com.example.demo.controller.UserController.getUserById(java.lang.Long)",
    "called": "com.example.demo.service.UserService.getUserById(java.lang.Long)",
    "execution_time": 46,
    "call_count": 8
  },
  {
    "caller": "com.example.demo.controller.UserController.getUserByUsername(java.lang.String)",
    "called": "com.example.demo.service.UserService.getUserByUsername(java.lang.String)",
    "execution_time": 343,
    "call_count": 8
  },
  {
    "caller": "com.example.demo.controller.UserController.registerUser(com.example.demo.model.User)",
    "called": "com.example.demo.service.UserService.registerUser(com.example.demo.model.User)",
    "execution_time": 68,
    "call_count": 9
  }
])

const graphicElements = ref([])
const chartOption = computed(() => ({
  tooltip: {},
  graphic: {
    elements: graphicElements.value,
  },
}))

const labelColors = [
  '#ff5722', '#3f51b5', '#4caf50', '#e91e63',
  '#009688', '#ff9800', '#9c27b0', '#795548'
]
const funcCoords = {}
const circles = []
const labels = []
const lines = []
const points = []
const placedCircles = []
const labelByCircle = {}


function buildChart() {
  const grouped = rawData.value.reduce((acc, cur) => {
    acc[cur.label] = acc[cur.label] || []
    acc[cur.label].push(cur)
    return acc
  }, {})

  const mergedConnections = rawConnections.value.reduce((acc, cur) => {
    const key = `${cur.caller}->${cur.called}`
    if (!acc[key]) {
      acc[key] = {
        caller_func: cur.caller,
        called_func: cur.called,
        call_count: cur.call_count,
        execution_time: cur.execution_time,
      }
    } else {
      acc[key].call_count += cur.call_count
      acc[key].execution_time += cur.execution_time
    }
    return acc
  }, {})

  const keys = Object.keys(grouped)
  const padding = 20

  const isCircleOverlapping = (cx, cy, r) =>
    placedCircles.some((c) => Math.sqrt((c.cx - cx) ** 2 + (c.cy - cy) ** 2) < c.r + r + padding)

  keys.forEach((label) => {
    const funcs = grouped[label]
    const funcCount = funcs.length
    const r = Math.max(50, Math.min(200, 20 + Math.sqrt(funcCount) * 60))

    let cx,
      cy,
      attempt = 0
    do {
      cx = Math.random() * 1000 + r
      cy = Math.random() * 600 + r
      attempt++
    } while (isCircleOverlapping(cx, cy, r) && attempt < 500)

    placedCircles.push({ cx, cy, r })
    labelByCircle[`${cx},${cy},${r}`] = parseInt(label)

    circles.push({
      type: 'circle',
      shape: { cx, cy, r },
      style: { fill: '#f5f5f5', stroke: '#f5f5f5', lineWidth: 1 },
    })

    labels.push({
      type: 'text',
      left: cx - r,
      top: cy - r - 10,
      style: {
        text: `微服务 ${label}`,
        fill: '#333',
        font: 'bold 14px sans-serif',
      },
    })

    funcs.forEach((f, i) => {
      const angle = ((2 * Math.PI) / funcs.length) * i+50
      const pr = r * 0.7
      const px = cx + pr * Math.cos(angle)
      const py = cy + pr * Math.sin(angle)
      const radius = 8
      const color = labelColors[f.label % labelColors.length]

      funcCoords[f.func_name] = { x: px, y: py }

      const group = {
        id: `group-${f.func_name}`,
        type: 'group',
        position: [0, 0],
        draggable: true,
        children: [
          {
            type: 'circle',
            shape: { cx: px, cy: py, r: radius },
            style: { fill: color },
            // 添加 onmouseover 和 onmouseout 事件来显示和隐藏 tooltip
            onmouseover: () => {
              // 显示 tooltip，并传递当前点的位置（px, py）
              showTooltip(f.func_name, px, py)
            },
            onmouseout: () => {
              // 隐藏 tooltip
              hideTooltip()
            },
          },
          {
            type: 'text',
            left: px + 10,
            top: py - 5,
            style: {
              text: f.func_name,
              fill: '#000',
              font: '12px sans-serif',
            },
          },
        ],
        ondrag(e) {
          const dx = e.event.offsetX
          const dy = e.event.offsetY
          funcCoords[f.func_name] = { x: dx, y: dy }

          const circle = group.children.find((c) => c.type === 'circle')
          const text = group.children.find((t) => t.type === 'text')
          if (circle) {
            circle.shape.cx = dx
            circle.shape.cy = dy
          }
          if (text) {
            text.left = dx + 10
            text.top = dy - 5
          }

          updateLines(f.func_name)
        },
        ondragend(e) {
          const dx = e.event.offsetX
          const dy = e.event.offsetY
          const inside = placedCircles.find(
            (c) => Math.sqrt((dx - c.cx) ** 2 + (dy - c.cy) ** 2) < c.r,
          )

          const keys = Object.values(labelByCircle)

          if (!inside) {
            const newLabel = Math.max(...keys.map(Number), 0) + 1
            const newR = 60

            placedCircles.push({ cx: dx, cy: dy, r: newR })
            labelByCircle[`${dx},${dy},${newR}`] = newLabel
            f.label = newLabel

            circles.push({
              type: 'circle',
              shape: { cx: dx, cy: dy, r: newR },
              style: { fill: '#f5f5f5', stroke: '#f5f5f5', lineWidth: 1 },
            })

            labels.push({
              type: 'text',
              left: dx - newR,
              top: dy - newR - 15,
              style: {
                text: `微服务 ${newLabel}`,
                fill: '#333',
                font: 'bold 14px sans-serif',
              },
            })
          } else {
            f.label = labelByCircle[`${inside.cx},${inside.cy},${inside.r}`]
          }

          // 🧹 删除没有元素使用的圈和标签
          const activeLabels = rawData.value.map((item) => item.label)
          const toDelete = placedCircles.filter((c) => {
            const label = labelByCircle[`${c.cx},${c.cy},${c.r}`]
            return !activeLabels.includes(label)
          })

          for (const c of toDelete) {
            const label = labelByCircle[`${c.cx},${c.cy},${c.r}`]

            // 删除 placedCircles
            const pcIndex = placedCircles.findIndex(
              (item) => item.cx === c.cx && item.cy === c.cy && item.r === c.r,
            )
            if (pcIndex !== -1) placedCircles.splice(pcIndex, 1)

            // 删除 circle 图形
            const circleIndex = circles.findIndex(
              (item) => item.shape?.cx === c.cx && item.shape?.cy === c.cy && item.shape?.r === c.r,
            )
            if (circleIndex !== -1) circles.splice(circleIndex, 1)

            // ✅ 更稳妥地删除标签（通过 label 文本匹配）
            const labelIndex = labels.findIndex((item) => item.style?.text === `微服务 ${label}`)
            if (labelIndex !== -1) labels.splice(labelIndex, 1)

            // 删除映射
            delete labelByCircle[`${c.cx},${c.cy},${c.r}`]
          }

          graphicElements.value = [...circles, ...points, ...labels, ...lines]
        },

        tooltip: {
          formatter: () => `
        <b>${f.func_name}</b><br/>
        文件: ${f.file_path}<br/>
        行: ${f.lineno}-${f.end_lineno}<br/>
        时间: ${f.execution_time}ms<br/>
        次数: ${f.count}
      `,
        },
      }

      points.push(group)
    })

    // 显示工具提示
    function showTooltip(func_name,x, y) {
      const tooltip = document.getElementById('tooltip');
      tooltip.style.left = `${x + 15}px`; // 偏移一定距离，以避免覆盖图形
      tooltip.style.top = `${y + 15}px`;
      tooltip.style.display = 'block';
      tooltip.innerHTML = `
    <b>${func_name}</b><br/>
  `;
    }

// 隐藏工具提示
    function hideTooltip() {
      const tooltip = document.getElementById('tooltip');
      tooltip.style.display = 'none';
    }


  })

  Object.values(mergedConnections).forEach((conn) => {
    const from = funcCoords[conn.caller_func]
    const to = funcCoords[conn.called_func]
    if (!from || !to) return
    const midX = (from.x + to.x) / 2
    const midY = (from.y + to.y) / 2 - 30

    lines.push({
      id: `line-${conn.caller_func}->${conn.called_func}`,
      type: 'group',
      caller_func: conn.caller_func,
      called_func: conn.called_func,
      children: [
        {
          type: 'bezierCurve',
          shape: {
            x1: from.x,
            y1: from.y,
            x2: to.x,
            y2: to.y,
            cpx1: midX,
            cpy1: midY,
          },
          style: {
            stroke: '#00c853',
            lineWidth: Math.min(10, conn.call_count),
          },
          onmouseover: () => {
            // 当鼠标悬停在这条线时显示 tooltip
            const lineTooltip = `
            <b>${conn.caller_func} -> ${conn.called_func}</b><br/>
            调用次数: ${conn.call_count}<br/>
            执行时间: ${conn.execution_time}ms
          `;
            showTooltip(lineTooltip, midX, midY);  // 使用线条的中点位置显示 tooltip
          },
          onmouseout: () => {
            // 隐藏 tooltip
            hideTooltip();
          },
        },
      ],
    })
  })

// 显示工具提示的函数，可以接受任意内容和位置
  function showTooltip(content, x, y) {
    const tooltip = document.getElementById('tooltip');
    tooltip.style.left = `${x + 15}px`; // 偏移一定距离，避免覆盖图形
    tooltip.style.top = `${y + 15}px`;
    tooltip.style.display = 'block';
    tooltip.innerHTML = content;
  }

// 隐藏工具提示
  function hideTooltip() {
    const tooltip = document.getElementById('tooltip');
    tooltip.style.display = 'none';
  }


  graphicElements.value = [...circles, ...points, ...labels, ...lines]
}

function updateLines(funcName) {
  lines.forEach((line) => {
    if (line.caller_func === funcName || line.called_func === funcName) {
      const from = funcCoords[line.caller_func]
      const to = funcCoords[line.called_func]
      const midX = (from.x + to.x) / 2
      const midY = (from.y + to.y) / 2 - 30
      const bezier = line.children[0]
      bezier.shape.x1 = from.x
      bezier.shape.y1 = from.y
      bezier.shape.x2 = to.x
      bezier.shape.y2 = to.y
      bezier.shape.cpx1 = midX
      bezier.shape.cpy1 = midY
    }
  })
  graphicElements.value = [...circles, ...points, ...labels, ...lines]
}

onMounted(buildChart)
</script>
