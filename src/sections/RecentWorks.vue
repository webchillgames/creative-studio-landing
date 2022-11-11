<template>
  <div class="s-recent-works">
    <div class="s-recent-works__main-title" ref="titleRef">
      <h2>Recent works</h2>
    </div>
    <p class="s-recent-works__subtitle">We Offer Digital Solutions</p>

    <div
      class="s-recent-works__work work"
      v-for="v in DATA"
      :key="v.id"
      ref="workRef"
    >
      <div class="work__block work__block--text">
        <p class="work__type">{{ v.type }}</p>
        <h3 class="work__title">
          <span v-for="(t, i) in v.title" :key="i">{{ t }}</span>
        </h3>

        <p ref="textRef" class="work__text">{{ v.text }}</p>

        <CButton />
      </div>

      <div class="work__block work__block--img">
        <img :src="v.img" :alt="v.imgAlt" />
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";
// import { onIntersect } from "@/composables/onIntersect";
import { RECENT_WORKS as DATA } from "@/data.js";
import CButton from "../components/CButton.vue";

export default {
  components: { CButton },
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
    };
  },
};
</script>

<style lang="scss" scoped>
.s-recent-works {
  padding-top: 120px;
  text-align: center;

  &__main-title {
    @include coveredText($dark-color);
    @include BlockCoveringText(#fff, 0.5s, 0s);

    h2 {
      font-size: 50px;
      line-height: 55px;
      font-weight: 600;
      text-transform: uppercase;
      margin: 0;
    }
  }

  &__subtitle {
    opacity: 0;
    transition: opacity 0.5s ease-in 0.3s;

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
  display: flex;

  padding-bottom: 90px;

  &:nth-child(2n) {
    .work__block--text {
      order: 1;
    }
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

  &__title {
    display: flex;
    flex-direction: column;
    margin: 0;
    font-weight: 500;
    letter-spacing: 2px;
    line-height: 1;
    font-size: 28px;

    span {
      margin: 0;
      align-self: flex-start;
      letter-spacing: 1px;

      @include coveredText($dark-color);

      @include BlockCoveringText($dark-color, 0.2s, 0.2s);
    }

    span:nth-child(2) {
      @include BlockCoveringText($dark-color, 0.2s, 0.3s);
    }

    span:nth-child(3) {
      @include BlockCoveringText($dark-color, 0.3s, 0.4s);
    }

    span + span {
      margin-top: 4px;
    }
  }

  &__block {
    flex-shrink: 0;
    width: 50%;
    flex-basis: 50%;
    overflow: hidden;
    text-align: left;

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
    position: relative;
    background-color: #262626;

    img {
      width: 0;
      transition: width 0.5s ease-out 0.7s;
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
}

.s-recent-works__work.active {
  .work__type::after,
  .work__title span::after {
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
