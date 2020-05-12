<template>
  <div class="component s-dialog">
    <slot name="content"></slot>
    <slot name="close">
      <div @click="close()" class="close-btn">关闭 x</div>
    </slot>
  </div>
</template>

<script>
  import {VueExtend} from 'godspen-lib'

  export default {
    mixins: [VueExtend.mixin],
    name: 'simple-dialog',
    label: process.env.LABEL,
    style: process.env.STYLE,
    stack: true, // 是否是堆叠模式 ，false：孩子元素会按楼层一个个向下排布， true: 孩子元素绝对定位，随意放置位置
    slots: [
      {
        name: 'content',
        style: {
          margin: 'auto',
          position: 'absolute',
          left: 0,
          right: 0,
          top: 0,
          bottom: 0,
        }
      },
      {
        name: 'close',
        style: {}
      },
    ],
    mounted () {
    },
    editorMethods: {
      open: {
        label: '打开弹窗',
        params: []
      },
      close: {
        label: '关闭弹窗',
        params: []
      }
    },
    methods: {
      open () {
        var $com = this.getParent()
        $com.visible = true
      },
      getParent () {
        return process.env.NODE_ENV !== 'production' ? this.$parent.$parent : this.$parent
      },
      close () {
        var $com = this.getParent()
        $com.visible = false
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus" type="text/stylus" scoped>
  .component.s-dialog {
    position absolute
    left: 0
    right 0
    bottom 0
    top 0
    .close-btn {
      color: #fff;
      padding: 20px;
      font-size: 16px;
      cursor: pointer;
      position: absolute;
      right: 10px;
      top: 10px;
    }
  }
</style>
