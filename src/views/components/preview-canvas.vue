<template>
  <mu-dialog
    width="360"
    transition="slide-bottom"
    fullscreen
    :open.sync="open"
    dialog-class="mu-preview-canvas-dialog"
  >
    <mu-appbar
      :z-depth="2"
      color="#303030"
      text-color="#ddd"
      title="预览"
      class="mu-fixed-appbar"
    >
      <mu-button slot="right" icon @click="close">
        <mu-icon value="close"></mu-icon>
      </mu-button>
    </mu-appbar>
    <div
      class="canvas-wrapper"
      data-mu-loading-color="orange"
      data-mu-loading-overlay-color="#303030"
      data-mu-loading-text="正在生成预览效果，请稍等..."
      v-loading="loading"
    >
      <div style="padding: 1%; width: 98%; float: left;">
        <img :src="url" width="100%">
      </div>
    </div>
  </mu-dialog>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
import VarMixin from '@/mixins/var.js'
export default {
  name: 'PreviewCanvas',
  mixins: [
    VarMixin
  ],
  props: {
    open: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      url: '',
      loading: true
    }
  },
  computed: {
    ...mapGetters([
      'canvas'
    ])
  },
  mounted () {
    this.url = this.canvas.toDataURL({
      format: 'png',
      multiplier: 4
    })
    this.loading = false
  },
  methods: {
    ...mapActions([
      'setOpenPreviewCanvasDialog'
    ]),
    close () {
      // 初始化线模图
      this.showDieLineBg()
      this.setOpenPreviewCanvasDialog(false)
      // this.$emit('update:open')
    }
  }
}
</script>

<style lang="scss">
.mu-preview-canvas-dialog {
  .mu-dialog-body {
    height: 100%;
    overflow-y: auto;
    overflow-x: hidden;
    background-color: #5f5d5d;
  }
  canvas {
    display: block;
    margin: 0 auto;
  }
  .mu-fixed-appbar {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 999;
  }
  .canvas-wrapper {
    padding: 60px 0 30px 0;
  }
}
</style>
