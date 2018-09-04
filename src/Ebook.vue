<template>
    <div class="ebook">
        <transition name="slide-down">
            <div class="title-wrapper" v-show="ifTitleAndMenuShow">
                <div class="left">
                    <span class="icon-back icon"></span>
                </div>
                <div class="right">
                    <div class="icon-wrapper">
                        <span class="icon-cart icon"></span>
                    </div>
                    <div class="icon-wrapper">
                        <span class="icon-person icon"></span>
                    </div>
                    <div class="icon-wrapper">
                        <span class="icon-more icon"></span>
                    </div>
                </div>
            </div>
        </transition>
        <div class="read-wrapper">
            <div id="read"></div>
            <div class="mask">
                <div class="left" @click="prevPage"></div>
                <div class="center" @click="toggleTitleAndMenu"></div>
                <div class="right" @click="nextPage"></div>
            </div>
        </div>
        <transition name="slide-up">
            <div class="menu-wrapper" v-show="ifTitleAndMenuShow">
                <div class="icon-wrapper">
                    <div class="icon-menu icon"></div>
                </div>
                <div class="icon-wrapper">
                    <div class="icon-progress icon"></div>
                </div>
                <div class="icon-wrapper">
                    <div class="icon-bright icon"></div>
                </div>
                <div class="icon-wrapper">
                    <div class="icon-a icon">A</div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
import Epub from 'epubjs'
const DOWNLOAD_URL = '/static/2018_Book_AgileProcessesInSoftwareEngine.epub'

export default {
  data () {
    return {
      ifTitleAndMenuShow: false
    }
  },
  methods: {
    toggleTitleAndMenu () {
      this.ifTitleAndMenuShow = !this.ifTitleAndMenuShow
    },
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
    .title-wrapper {
        position: absolute;
        top: 0;
        left: 0;
        z-index: 101;
        display: flex;
        width: 100%;
        height: px2rem(48);
        background-color: white;
        box-shadow: 0 px2rem(8) px2rem(8) rgba(0, 0, 0, .15);
        .left {
            flex: 0 0 px2rem(60);
            @include center;
        }
        .right {
            flex: 1;
            display: flex;
            justify-content: flex-end;
            .icon-wrapper {
                flex: 0 0 px2rem(40);
                @include center;
                .icon-cart {
                    font-size: px2rem(22);
                }
            }
        }
    }
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
    .menu-wrapper {
        position: absolute;
        bottom: 0;
        left: 0;
        z-index: 101;
        display: flex;
        width: 100%;
        height: px2rem(48);
        background-color: white;
        box-shadow: 0 px2rem(-8) px2rem(8) rgba(0, 0, 0, .15);
        .icon-wrapper {
            flex: 1;
            @include center;
            .icon-progress {
                font-size: px2rem(28);
            }
            .icon-bright {
                font-size: px2rem(24);
            }
        }
    }
}

</style>
