<script setup>
import { RouterLink, RouterView } from "vue-router";
import TheHeader from "./components/TheHeader.vue";
import { useMouse, useScroll } from "@vueuse/core";
import { ref, watch, onMounted, onUpdated, toRefs, toRef } from "vue";

const el = ref(null);
const scrollingUp = ref();
const { y, directions, isScrolling, arrivedState } = useScroll(el);
onUpdated(() => {
  console.log(directions);
});
</script>

<template>
  <div class="scroll-container" ref="el">
    <the-header
      :scrollY="y"
      :scrollTop="directions.top"
      :isScrolling="isScrolling"
      :arrived="arrivedState.bottom"
    ></the-header>
  </div>
  <main></main>
</template>

<style scoped>
.scroll-container {
  max-height: 100vh;
  overflow-y: scroll;
}
</style>
