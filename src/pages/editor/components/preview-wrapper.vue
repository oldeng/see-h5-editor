<template>
  <div class="components-preview">
    <div class="setting-bg"></div>
    <div class="left-panel">
      <div class="iframe-wrapper"
           :style="{width: $config.canvasH5Width + 'px', height: $config.canvasH5Height + 'px'}">
        <iframe :src="previewUrl" frameborder="0"
                style="background-color:transparent;width: 100%; height: 100%;"></iframe>
      </div>
    </div>
    <span class="cloase-btn" @click="closePreview">
      <i class="el-icon-close"></i>
    </span>
  </div>
</template>

<script>
import $utils from '@/utils'

const { location: { origin, pathname } } = window

function findPath (pathname) {
  const last = pathname.lastIndexOf('/')
  return pathname.slice(0, last + 1)
}
const publicPath = findPath(pathname)

export default {
  name: 'preview-page',
  props: {
    pageId: String
  },
  computed: {
    previewUrl () {
      // 由于 github pages 部署不支持 history 模式，采用hash模式，实际项目建议使用 history 模式
      return `${origin}${publicPath}h5.html#/?${$utils.stringifyParams(this.globalVariable)}`
    }
  },
  data () {
    return {}
  },
  created () {
  },
  methods: {
    closePreview () {
      this.$emit('closePreview', false)
    }
  }
}
</script>

<style lang="scss" scoped>
  .components-preview-inner {
    width: 100%;
  }

  .setting-bg {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, .8);
    z-index: 1042;
  }

  .left-panel {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    z-index: 1050;
    overflow: hidden;
  }

  .right-panel {
    position: fixed;
    width: 640px;
    top: 0;
    right: 0;
    bottom: 0;
    z-index: 1050;
    background-color: #fff;
    overflow-y: auto;
    color: #333;
  }

  .iframe-wrapper {
    position: absolute;
    left: 50%;
    top: 50%;
    margin-left: -185px;
    margin-top: -334px;
    background: white;
  }

  .cloase-btn {
    position: fixed;
    top: 8px;
    right: 20px;
    font-size: 28px;
    color: #7F8593;
    -webkit-transition: all 0.28s;
    transition: all 0.28s;
    z-index: 1060;
    cursor: pointer;

    &:hover {
      color: $primary;
    }
  }
</style>
