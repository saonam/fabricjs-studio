<template>
  <div class="studio-page">
    <!-- 头部 -->
    <app-header/>
    <!-- 主体容器 -->
    <main class="main-container">
      <!-- 左侧边栏 -->
      <app-sidebar/>
      <!-- 中间主体内容 -->
      <app-main/>
      <!-- 右侧边栏 -->
      <app-rside/>
    </main>
    <!-- 预览画布效果 -->
    <preview-canvas v-if="openPreviewCanvasDialog" :open.sync="openPreviewCanvasDialog"/>
  </div>
</template>

<script>
import { AppHeader, AppSidebar, AppMain, AppRside } from './layout'
import { mapGetters } from 'vuex'
import PreviewCanvas from './components/preview-canvas.vue'

export default {
  name: 'studio-page',
  components: {
    AppHeader,
    AppSidebar,
    AppMain,
    AppRside,
    PreviewCanvas
  },
  computed: {
    ...mapGetters([
      'openPreviewCanvasDialog'
    ])
  }
}
</script>
