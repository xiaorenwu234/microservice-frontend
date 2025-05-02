<template>
  <CircleLayout v-model:rawData="rawData" v-model:rawConnections="rawConnections"></CircleLayout>
</template>

<script setup>
import CircleLayout from './components/chart.vue'
import { ref } from 'vue'

const rawData = ref([
  {
    "func_name": "Config",
    "file_path": "examples/flask_demo/config",
    "lineno": 25,
    "end_lineno": 28,
    "docstring": null,
    "execution_time": 0,
    "count": 0,
    "label": 4
  },
  {
    "func_name": "Product",
    "file_path": "examples/flask_demo/models/product_model",
    "lineno": 7,
    "end_lineno": 27,
    "docstring": null,
    "execution_time": 0,
    "count": 1,
    "label": 5
  },
  {
    "func_name": "OrderService",
    "file_path": "examples/flask_demo/services/order_service",
    "lineno": 10,
    "end_lineno": 29,
    "docstring": null,
    "execution_time": 82,
    "count": 5,
    "label": 0
  },
  {
    "func_name": "main",
    "file_path": "examples/flask_demo/app",
    "lineno": 33,
    "end_lineno": 37,
    "docstring": null,
    "execution_time": 25634,
    "count": 2,
    "label": 4
  },
  {
    "func_name": "UserController",
    "file_path": "examples/flask_demo/controllers/user_controller",
    "lineno": 7,
    "end_lineno": 30,
    "docstring": null,
    "execution_time": 101,
    "count": 5,
    "label": 6
  },
  {
    "func_name": "patch_trace",
    "file_path": "examples/flask_demo/patch_trace",
    "lineno": 10,
    "end_lineno": 63,
    "docstring": null,
    "execution_time": 0,
    "count": 0,
    "label": 1
  },
  {
    "func_name": "ProductController",
    "file_path": "examples/flask_demo/controllers/product_controller",
    "lineno": 7,
    "end_lineno": 30,
    "docstring": null,
    "execution_time": 87,
    "count": 5,
    "label": 5
  },
  {
    "func_name": "User",
    "file_path": "examples/flask_demo/models/user_model",
    "lineno": 6,
    "end_lineno": 22,
    "docstring": null,
    "execution_time": 0,
    "count": 1,
    "label": 6
  },
  {
    "func_name": "testcase",
    "file_path": "examples/flask_demo/tmp",
    "lineno": 4,
    "end_lineno": 6,
    "docstring": null,
    "execution_time": 0,
    "count": 8,
    "label": 0
  },
  {
    "func_name": "ProductService",
    "file_path": "examples/flask_demo/services/product_service",
    "lineno": 10,
    "end_lineno": 28,
    "docstring": null,
    "execution_time": 76,
    "count": 5,
    "label": 5
  },
  {
    "func_name": "Weight",
    "file_path": "examples/flask_demo/controllers/order_controller",
    "lineno": 8,
    "end_lineno": 9,
    "docstring": null,
    "execution_time": 0,
    "count": 0,
    "label": 3
  },
  {
    "func_name": "OrderController",
    "file_path": "examples/flask_demo/controllers/order_controller",
    "lineno": 12,
    "end_lineno": 35,
    "docstring": null,
    "execution_time": 93,
    "count": 5,
    "label": 0
  },
  {
    "func_name": "DatabaseManager",
    "file_path": "examples/flask_demo/utils/database",
    "lineno": 7,
    "end_lineno": 14,
    "docstring": null,
    "execution_time": 1,
    "count": 2,
    "label": 2
  },
  {
    "func_name": "Order",
    "file_path": "examples/flask_demo/models/order_model",
    "lineno": 7,
    "end_lineno": 28,
    "docstring": null,
    "execution_time": 0,
    "count": 1,
    "label": 0
  },
  {
    "func_name": "UserService",
    "file_path": "examples/flask_demo/services/user_service",
    "lineno": 10,
    "end_lineno": 28,
    "docstring": null,
    "execution_time": 86,
    "count": 5,
    "label": 6
  }
])

const rawConnections = ref([
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/user_controller",
      "UserController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "execution_time": 10,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/product_controller",
      "ProductController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "execution_time": 10,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/order_controller",
      "OrderController",
      12,
      35,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "execution_time": 11,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/order_controller",
      "OrderController",
      12,
      35,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "execution_time": 8,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/product_controller",
      "ProductController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "execution_time": 9,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/user_controller",
      "UserController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "execution_time": 9,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/user_controller",
      "UserController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "execution_time": 11,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/product_controller",
      "ProductController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "execution_time": 10,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/order_controller",
      "OrderController",
      12,
      35,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "execution_time": 12,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/order_controller",
      "OrderController",
      12,
      35,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "execution_time": 11,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/tmp",
      "testcase",
      4,
      6,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/product_controller",
      "ProductController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "execution_time": 10,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/user_controller",
      "UserController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "execution_time": 12,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/order_controller",
      "OrderController",
      12,
      35,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "execution_time": 40,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/order_service",
      "OrderService",
      10,
      29,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/models/order_model",
      "Order",
      7,
      28,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/product_controller",
      "ProductController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "execution_time": 37,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/product_service",
      "ProductService",
      10,
      28,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/models/product_model",
      "Product",
      7,
      27,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/controllers/user_controller",
      "UserController",
      7,
      30,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "execution_time": 44,
    "call_count": 1
  },
  {
    "caller_tuple": [
      "examples/flask_demo/services/user_service",
      "UserService",
      10,
      28,
      null
    ],
    "called_tuple": [
      "examples/flask_demo/models/user_model",
      "User",
      6,
      22,
      null
    ],
    "execution_time": 0,
    "call_count": 1
  }
])
</script>
