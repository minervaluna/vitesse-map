<script setup lang="ts">
import AMapLoader from '@amap/amap-jsapi-loader'
import { onMounted, onUnmounted } from 'vue'

const vars = {
  center: {
    lnt: 121.551787,
    lat: 31.318956,
  },
  zoom: 14,
}

const map = ref<any>()
const mapRef = ref<HTMLDivElement>()

function renderMap() {
  AMapLoader.load({
    key: 'a01f05bd8b80ca883a806344808b8e07', // 申请好的Web端开发者Key，首次调用 load 时必填
    version: '2.0', // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
    plugins: ['AMap.Scale', 'AMap.ToolBar', 'AMap.MouseTool'], // 需要使用的的插件列表，如比例尺'AMap.Scale'等
    Loca: {
      version: '2.0.0',
    },
  })
    .then((AMap) => {
      map.value = new AMap.Map(mapRef.value, {
        center: [vars.center.lnt, vars.center.lat],
        zoom: vars.zoom, // 初始化地图级别
      })
      map.value.setFitView()
    })
    .catch((_e) => {
    // error...
    })
}

onMounted(() => {
  renderMap()
})

onUnmounted(() => {
  map.value?.destroy()
})
</script>

<template>
  <div ref="mapRef" h-full w-full />
</template>
