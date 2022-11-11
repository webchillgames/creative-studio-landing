<template>
  <div class="s-about-us" ref="sectionRef">
    <div class="s-about-us__titles">
      <div
        v-for="v in DATA.titles"
        :key="v.id"
        class="s-about-us__title"
        :data-text="v.text"
        ref="titleRef"
      >
        {{ v.text }}
      </div>
    </div>

    <div class="paragraphs">
      <p v-for="v in DATA.paragraphs" :key="v.id">
        {{ v.text }}
      </p>
    </div>

    <p class="paragraphs__message">{{ DATA.message }}</p>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";

import { ABOUT_US as DATA } from "@/data.js";

export default {
  setup() {
    const sectionRef = ref({});

    const titleObserver = new IntersectionObserver(
      (entries) => {
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
      titleObserver.observe(sectionRef.value);
    });

    return {
      DATA,
      sectionRef,
    };
  },
};
</script>

<style lang="scss">
.s-about-us {
  padding: 120px 20px;
  background-color: #000;

  &__title:first-child {
    &::after {
      transition: width 1s ease-out;
    }
  }

  &__title:last-child {
    &::after {
      transition: width 0.6s ease-out;
    }
  }

  &__title {
    text-transform: uppercase;
    position: relative;
    font-size: 50px;
    line-height: 65px;
    font-weight: 600;

    &::after {
      color: $accent-color;
      width: 0;
    }

    &::before {
      color: #fff;
    }

    &::after,
    &::before {
      position: absolute;
      top: 0;
      left: 0;
      content: attr(data-text);
      white-space: nowrap;
      overflow: hidden;
    }
  }

  &__titles {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
}

.paragraphs {
  display: flex;

  &__message {
    margin: 0;
    margin-top: 60px;
    color: #fff;
    text-align: center;
    font-weight: 400;
    letter-spacing: 5px;

    transform: translate3d(0, 5%, 0);
    opacity: 0;

    @include animation(slideUp, 0.3s, ease-out, 1, forwards, _, 0.9s);
  }

  p {
    color: #fff;
    font-size: 16px;
    line-height: 1.8;
    font-weight: 600;
    letter-spacing: 0px;
    font-family: "Open Sans", sans-serif;

    transform: translate3d(0, 10%, 0);
    opacity: 0;

    @include animation(slideUp, 0.6s, ease-out, 1, forwards, _, _);
  }

  p + p {
    margin-left: 30px;
  }

  p:first-child {
    animation-delay: 0.5s;
  }

  p:last-child {
    animation-delay: 0.7s;
  }
}

.s-about-us.active {
  .s-about-us__title::after {
    width: 100%;
  }
}
</style>
