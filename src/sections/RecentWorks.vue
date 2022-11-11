<template>
  <div class="s-recent-works">
    <div class="container small">
      <div class="s-recent-works__main-title" ref="titleRef">
        <h2>Recent works</h2>
      </div>
      <p class="s-recent-works__subtitle">We Offer Digital Solutions</p>
    </div>
    <div
      class="s-recent-works__work work"
      v-for="v in DATA"
      :key="v.id"
      ref="workRef"
    >
      <div class="container small work__container">
        <div class="work__block work__block--text">
          <div>
            <p class="work__type">{{ v.type }}</p>
            <!-- <h3 class="work__title">
              <span v-for="(t, i) in v.title" :key="i">{{ t }}</span>
            </h3> -->

            <CColoringTitle :text="v.title" />

            <p ref="textRef" class="work__text">{{ v.text }}</p>
          </div>

          <CButton />
        </div>

        <div class="work__block work__block--img">
          <img :src="v.img" :alt="v.imgAlt" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
// import { onIntersect } from "@/composables/onIntersect";

import { RECENT_WORKS as DATA } from "@/data.js";

import CButton from "@/components/CButton.vue";
import CColoringTitle from "../components/CColoringTitle.vue";

export default {
  components: { CButton, CColoringTitle },
  setup() {
    const workRef = ref([]);
    const textRef = ref([]);
    const titleRef = ref([]);

    const worksObserver = new IntersectionObserver(
      function (entries) {
        if (entries[0] && entries[0].isIntersecting) {
          entries[0].target.classList.add("active");
        }
      },
      {
        root: null,
        rootMargin: "0px",
        threshold: 0.2,
      }
    );

    const titleObserver = new IntersectionObserver(
      function (entries) {
        if (entries[0] && entries[0].isIntersecting) {
          entries[0].target.classList.add("active");
        }
      },
      {
        root: null,
        rootMargin: "0px",
        threshold: 0.2,
      }
    );

    onMounted(() => {
      for (let w of workRef.value) {
        worksObserver.observe(w);
      }

      titleObserver.observe(titleRef.value);
    });

    return {
      workRef,
      titleRef,
      // blockRef,
      textRef,
      DATA,
      CButton,
      CColoringTitle,
    };
  },
};
</script>

<style lang="scss">
.s-recent-works {
  padding-top: 120px;
  text-align: center;
  position: relative;

  &__main-title {
    @include coveredText($dark-color);
    @include BlockCoveringText(#fff, 0.5s, 0s);

    h2 {
      text-transform: uppercase;
      margin: 0;
      font-size: 65px;
      line-height: 1;
      font-weight: 600;
      letter-spacing: -2px;
    }
  }

  &__subtitle {
    text-transform: uppercase;
    font-size: 12px;
    line-height: 1.4;
    font-weight: 600;
    letter-spacing: 1px;
    opacity: 0;
    transition: opacity 0.5s ease-in 0.3s;
    margin-bottom: 60px;
    margin-top: 5px;

    position: relative;
  }

  &__main-title.active {
    &::after {
      transform: translate3d(100%, 0, 0);
    }

    & + .s-recent-works__subtitle {
      opacity: 1;
    }
  }
}

.work {
  padding-bottom: 90px;
  position: relative;

  &__container {
    display: flex;
  }

  &__wrapper {
    position: absolute;
  }

  &__type {
    margin: 0;
    margin-bottom: 4px;
    text-transform: uppercase;
    font-size: 14px;
    line-height: 1.4;
    font-weight: 600;
    letter-spacing: 0px;

    @include coveredText($accent-color);

    @include BlockCoveringText($accent-color, 0.2s);
  }

  &__block {
    flex-shrink: 0;
    width: 50%;
    flex-basis: 50%;
    overflow: hidden;
    text-align: left;
    min-height: 70vh;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.2s ease-out;
    }

    &:hover img {
      transform: scale(1.2);
    }
  }

  &__block--img {
    background-color: #262626;
    position: static;

    img {
      width: 0;
      transition: width 0.5s ease-in 0.1s;
    }
  }

  &__block--text {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    box-sizing: border-box;
    padding: 20px;
    padding-bottom: 0;

    .c-button {
      max-width: 70%;
      margin-top: 40px;
      opacity: 0;
      transform: translate3d(0, 10%, 0);
    }

    .work__text {
      margin-top: 40px;
      color: #888888;
      font-size: 14px;
      line-height: 2.15;
      font-weight: 400;
      letter-spacing: 1px;
      font-family: "Open Sans", sans-serif;

      opacity: 0;
      transform: translate3d(0, 10%, 0);
    }
  }

  &:nth-child(2n) {
    .work__block--text {
      order: 1;
    }
  }
}

.s-recent-works__work.active {
  .work__type::after,
  .c-coloring-title span::after {
    transform: translate3d(110%, 0, 0);
  }

  .work__text {
    @include animation(slideUp, 0.4s, ease-out, 1, forwards, _, 0.3s);
  }

  .c-button {
    @include animation(slideUp, 0.2s, ease-out, 1, forwards, _, 1s);
  }

  .work__block--img img {
    width: 100%;
  }
}
</style>
