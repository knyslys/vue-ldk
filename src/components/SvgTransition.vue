<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    width="120%"
    height="100%"
    viewBox="0 0 1950 1080"
    class="page-transition"
    preserveAspectRatio="none"
  >
    <path
      id="Path_1"
      data-name="Path 1"
      d="M0,0H1916.952V466.286S0,789.333,0,466.286Z"
      transform="translate(0.5 0.5)"
      fill="red"
      stroke="#707070"
      stroke-width="1"
    />
  </svg>
</template>

<script setup>
import { onMounted } from "vue";
import anime from "animejs/lib/anime.es.js";

onMounted(() => {
  anime({
    targets: ".page-transition path",
    d: [
      {
        value: "M0,0H1916.952V466.286S0,1212.952,0,889.9Z",
        value: "M0,0H1901.858L1920,1082.19S0,1405.237,0,1082.19Z",
        value: "M0,0H1916.952V1079.143S0,1402.19,0,1079.143Z",
      },
    ],
    duration: 5000,
  });
});
</script>

<style scoped>
.page-transition {
  position: fixed;
  z-index: 500;
  pointer-events: none;
  fill: red;

  top: 0;
  left: 0;
}
</style>
