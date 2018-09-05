<template>
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
</template>

<script>
export default {
  props: {
    ifTitleAndMenuShow: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style lang="scss" scoped>
@import '../assets/styles/global';

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
</style>
