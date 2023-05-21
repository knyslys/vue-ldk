<template>
  <header class="header relative" ref="el">
    <svg-transition v-if="changePage"> </svg-transition>
    <img
      src="headerparallax/mainheader.jpg"
      class="header-image absolute top-0 left-0 w-full h-full block"
      ref="headerel"
    />
    <img
      src="headerparallax/tree.png"
      class="tree tree-1 absolute bottom-0 max-w-[40%] left-0 block z-10"
    />
    <img
      src="headerparallax/tree.png"
      class="tree tree-2 absolute bottom-[0] right-0 max-w-[45vh] block z-20"
    />
    <img
      src="headerparallax/birds.png"
      ref="birdEl"
      class="birds absolute top-1/4 left-2/4 max-w-[25%] block"
    />
    <img
      src="headerparallax/ducks.png"
      class="ducks absolute bottom-1/4 left-2/4 max-w-[25%] block z-0 opacity-80"
    />
    <div
      class="logo absolute bottom-[50vh] left-2/4 -translate-x-2/4 z-10 w-full text-center"
      v-if="showLogo"
    >
      <h1 class="logo-text text-4xl" @click="nextPage">
        Grand Duchy of Lithuania
      </h1>
    </div>

    <div class="section"></div>
  </header>
</template>

<script setup>
import anime from "animejs/lib/anime.es.js";
import { useMouse, useScroll } from "@vueuse/core";
import { ref, watch, onMounted, onUpdated, toRefs, toRef } from "vue";
import SvgTransition from "./SvgTransition.vue";
const props = defineProps({
  scrollY: {
    type: Number,
  },
  scrollTop: {
    type: Boolean,
  },
  isScrolling: {
    type: Boolean,
  },
  arrived: {
    type: Boolean,
  },
});

const el = ref(null);
const headerel = ref(null);
const birdEl = ref(null);

const { x, y } = useMouse();
const mouseX = toRef(x);
const mouseY = toRef(y);
const scroll = useScroll(el);
const showLogo = ref(false);
const changePage = ref(false);

const nextPage = () => {
  changePage.value = true;
};

// const scrollY = toRef(scroll.value.y);
onUpdated(() => {
  let modifier = props.scrollTop === true ? 1 : -1;
  if (props.arrived) showLogo.value = true;
  anime({
    targets: ".header-image",
    perspective: 2500,
    translateZ: props.scrollY * 0.55,
  });
  anime({
    targets: ".tree-1",
    perspective: 2500,
    translateZ: props.scrollY * 0.55,
    translateX: props.scrollY * -1 * 0.025,
  });

  anime({
    targets: ".tree-2",
    perspective: 1500,
    translateZ: props.scrollY * 0.15,
    translateX: props.scrollY * -1 * 0.025,
  });

  anime({
    targets: ".birds",
    perspective: 1500,
    translateZ: props.scrollY * 2 * -1,
    translateX: props.scrollY * 0.925,
    translateY: props.scrollY * -0.225,
    opacity: function (el) {
      if (!props.scrollTop && props.isScrolling) {
        let scrollValue = (props.scrollY / 100) * 0.2;
        console.log("scrolvalue " + scrollValue);
        return scrollValue * 0.25;
      }
      if (props.scrollTop && props.isScrolling) {
        return 1;
      }
    },
    duration: 3000,
  });

  anime({
    targets: ".ducks",
    perspective: 1500,
    translateZ: props.scrollY * 0.55,
    translateX: props.scrollY * -0.5 * 0.525,
  });

  anime({
    targets: ".header-image",
  });
});
</script>

<style scoped>
.section {
  height: 2000px;
}
.header-image {
  transform: perspective(1500px) translateZ(100px);
  object-fit: cover;
}

.header {
  min-height: 100vh;
  overflow-x: hidden;
  overflow-y: hidden;
}

.logo-text {
  font-size: 5rem;
}
</style>
