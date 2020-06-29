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
  </div>
</template>

<script>
export default {
  mounted() {
    const controller = new this.$scrollmagic.Controller();

    const scene1 = new this.$scrollmagic.Scene({
      triggerElement: this.$refs.pageContainer,
      triggerHook: 1,
      duration: window.innerHeight - 100,
      offset: 100
    })
      .on('progress', e => {
        console.log(e.progress);

        this.$refs.pageElement.style.top = `${ e.progress * (window.innerHeight - 100) }px`;
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
      background: #ff0000;
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
    }
  }
</style>
