<template>
  <div class="page">
    <div
      class="page__container"
      ref="pageContainer"
    >
      <div
        :class="{
          'page__element': true,
          'page__element--top': top,
          'page__element--bottom': bottom,
          'page__element--fixed': fixed
        }"
        ref="pageElement"
      ></div>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      top: true,
      bottom: false,
      fixed: false
    }
  },
  mounted() {
    const containerSizes = this.$refs.pageContainer.getBoundingClientRect();
    const elementSizes = this.$refs.pageElement.getBoundingClientRect();

    const controller = new this.$scrollmagic.Controller();

    const scene1 = new this.$scrollmagic.Scene({
      triggerElement: this.$refs.pageContainer,
      triggerHook: 1,
      duration: containerSizes.height - elementSizes.height,
      offset: elementSizes.height
    })
      .on('progress', e => {

        if (e.progress == 1 || e.progress == 0) {
          this.fixed = false;
          this.top = e.progress == 0 ? true : false;
          this.bottom = e.progress == 1 ? true : false;
        } else {
          this.fixed = true;
          this.top = false;
          this.bottom = false;
        }
      });

    controller.addScene([scene1]);
  }
}
</script>

<style lang="scss">
  .page {

    &__container {
      height: 100vh;
      //width: 900px;
      margin: 100vh auto 100vh;
      background: #EEEEEE;
      position: relative;
    }

    &__element {
      width: 150px;
      height: 100px;
      background-color: #000000;
      background-image: url("~static/businessman.jpg");
      background-repeat: no-repeat;
      background-size: contain;
      position: absolute;
      left: 50%;
      transform: translateX(-50%);

      &--top {
        position: absolute;
        top: 0;
      }

      &--bottom {
        position: absolute;
        bottom: 0;
      }

      &--fixed {
        position: fixed;
        bottom: 0;
      }

    }
  }
</style>
