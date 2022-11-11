<template>
  <div>
    <AboutUs ref="aboutUsRef" />
    <RecentWorks ref="scrollRef" />
    <OurClients />
  </div>
</template>

<script>
import AboutUs from "@/sections/AboutUs.vue";
import RecentWorks from "@/sections/RecentWorks.vue";

import { onIntersect } from "./composables/onIntersect";
import { onMounted, onUnmounted, ref } from "vue";
import OurClients from './sections/OurClients.vue';

export default {
  components: { AboutUs, RecentWorks, OurClients },

  setup() {
    const observer = ref({});
    const scrollRef = ref({});
    const aboutUsRef = ref({});

    // function onEnter() {
    //   console.log("start");
    //   const title = document.querySelector(".s-recent-works__main-title");
    //   title.classList.add("active");
    // }

    // function onExit() {
    //   console.log("finish");
    //   // const title = document.querySelector(".s-recent-works__main-title");
    //   // title.classList.remove("active");
    // }
    // const title = ref(document.querySelector(".s-recent-works__main-title"));

    const IntersectTitle = {
      onEnter() {
        // title.value.classList.add("active");
      },
      onExit() {},
    };

    onMounted(() => {
      observer.value = onIntersect(
        scrollRef.value.$el,
        IntersectTitle.onEnter,
        IntersectTitle.onExit,
        false,
        {
          threshold: 0.1,
        }
      );
    });

    onUnmounted(() => {
      observer.value.disconnect();
    });

    return {
      AboutUs,
      RecentWorks,
      scrollRef,
      aboutUsRef,
      OurClients,
    };
  },
};
</script>

<style lang="scss">
@import "@/styles/style.scss";
</style>
