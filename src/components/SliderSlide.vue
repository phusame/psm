<template>
  <Transition :name="transition">
    <div v-if="dirty" v-show="active" class="SliderSlide">
      <slot />
    </div>
  </Transition>
</template>

<script>
/* https://markus.oberlehner.net/blog/building-a-simple-content-slider-with-vue/ */
export default {
  name: "SliderSlide",
  data() {
    return {
      active: false,
      dirty: false,
      transition: "",
    };
  },
  methods: {
    // Deactivate and hide the slide and
    // also activate the correct transition.
    hide(direction) {
      this.transition = `SliderSlide--transition-${direction}`;
      this.active = false;
    },
    // Activate and show the slide and
    // also activate the correct transition.
    show(direction) {
      this.transition = `SliderSlide--transition-${direction}`;
      this.active = true;
      this.dirty = true;
    },
  },
};
</script>

<style lang="postcss">
.SliderSlide {
  /* @apply w-full; */
}

.SliderSlide--transition-left-enter-active,
.SliderSlide--transition-left-leave-active,
.SliderSlide--transition-right-enter-active,
.SliderSlide--transition-right-leave-active {
  transition-duration: 0.75s;
  /* transition-property: height, opacity, transform; */
  transition-property: height, opacity;
  /* transition-timing-function: cubic-bezier(0.55, 0, 0.1, 1); */
  transition-timing-function: theme(bezier.thisalso);
  overflow: hidden;
}

.SliderSlide--transition-left-leave-active,
.SliderSlide--transition-right-leave-active {
  top: 0;
  position: absolute;
}

.SliderSlide--transition-left-enter,
.SliderSlide--transition-right-leave-active {
  opacity: 0;
  /* transform: translate(2em, 0); */
}

.SliderSlide--transition-left-leave-active,
.SliderSlide--transition-right-enter {
  opacity: 0;
  /* transform: translate(-2em, 0); */
}
</style>
