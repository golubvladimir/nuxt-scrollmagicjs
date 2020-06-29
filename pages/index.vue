<template>
  <div class="page">
    <div
      class="page__container"
      ref="pageContainer"
    >
      <div
        class="page__element"
        ref="pageElement"
      ></div>
    </div>
    <div
      class="page__container"
      ref="pageSection"
    >
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    const containerSizes = this.$refs.pageContainer.getBoundingClientRect();

    const controller = new this.$scrollmagic.Controller();

    const scene1 = new this.$scrollmagic.Scene({
      triggerElement: this.$refs.pageContainer,
      triggerHook: 1,
      duration: containerSizes.height,
      offset: 100
    })
      .on('progress', e => {

        if (e.progress == 1 || e.progress == 0) {
          this.$refs.pageElement.style.position = 'absolute'
        } else {
          this.$refs.pageElement.style.position = 'fixed';
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
      margin: 100vh auto 0;
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
      position: fixed;
      bottom: 0;
    }
  }
</style>
