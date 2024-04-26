<template>
  <div id="cesiumContainer"></div>
</template>

<script setup>
import { onMounted } from 'vue';
import * as Cesium from 'cesium';

onMounted(() => {
  Cesium.Ion.defaultAccessToken =
    'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI3M2QxMjc3NC0yODUyLTQ3Y2MtODA2Zi00ZjgwNmUwOTUyYjMiLCJpZCI6MjExNDQyLCJpYXQiOjE3MTQxMDM1NjN9.UkrC7RA4JhHlqLYOGPN8hwoT6-SwfHmELGTXUukq_ik';
  // 自定义图层
  const custom = new Cesium.ArcGisMapServerImageryProvider({
    url: 'https://services.arcgisonline.com/arcgis/rest/services/World_Imagery/MapServer',
    enablePickFeatures: false
  });
  const viewer = new Cesium.Viewer('cesiumContainer', {
    imageryLayers: custom, // 自定义图层，默认谷歌的影响图层
    terrain: Cesium.Terrain.fromWorldTerrain({
      requestWaterMask: true
    }), // 地形图层
    timeline: false, // 时间控件
    animation: false, // 动画控件
    geocoder: false, // 搜索按钮
    homeButton: false, // 主页按钮
    sceneModePicker: false, // 投影方式按钮
    baseLayerPicker: false, // 图层选择按钮
    navigationHelpButton: false, // 帮助手势按钮
    fullscreenButton: false // 全屏按钮
  });
  // Cesium.Cartesian3.fromDegrees(116.39, 39.9, 500);
  // 设置初始位置
  // viewer.camera.setView({
  //   destination: Cesium.Cartesian3.fromDegrees(116.39, 39.9, 1000)
  // });
});
</script>

<style>
#cesiumContainer {
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
  overflow: hidden;
}

.cesium-viewer-bottom {
  display: none;
}
</style>
