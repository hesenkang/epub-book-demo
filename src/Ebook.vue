<template>
    <div class="ebook">
        <div class="read-wrapper">
            <div id="read"></div>
            <div class="mask">
                <div class="left" @click="prevPage"></div>
                <div class="center"></div>
                <div class="right" @click="nextPage"></div>
            </div>
        </div>
    </div>
</template>

<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'

export default {
  methods: {
    prevPage () {
      // this.rendition.prev
      if (this.rendition) {
        this.rendition.prev()
      }
    },
    nextPage () {
      // this.rendition.next
      if (this.rendition) {
        this.rendition.next()
      }
    },
    // 电子书解析和渲染
    showEpub () {
      // 生成Book
      this.book = new Epub(DOWNLOAD_URL)
      console.log(this.book)
      // 生成Rendtion，通过Book.renderTo
      this.rendition = this.book.renderTo('read', {
        width: window.innerWidth,
        height: window.innerHeight
      })
      // 通过Rendtion.display渲染电子书
      this.rendition.display()
    }
  },
  mounted () {
    this.showEpub()
  }
}

</script>

<style lang='scss' scoped>
@import 'assets/styles/global';

.ebook {
    position: relative;
    .read-wrapper {
        .mask {
            position: absolute;
            top: 0;
            left: 0;
            z-index: 100;
            width: 100%;
            height: 100%;
            display: flex;
            .left {
                flex: 0 0 px2rem(100);
            }
            .center {
                flex: 1;
            }
            .right {
                flex: 0 0 px2rem(100);
            }
        }
    }
}

</style>
