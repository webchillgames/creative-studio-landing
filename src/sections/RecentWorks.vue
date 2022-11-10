<template>
  <div class="s-recent-works">
    <div class="s-recent-works__main-title" ref="titleRef">
      <h2>Recent works</h2>
    </div>
    <p class="s-recent-works__subtitle">We Offer Digital Solutions</p>

    <div
      class="s-recent-works__work"
      v-for="v in DATA"
      :key="v.id"
      ref="workRef"
    >
      <div class="s-recent-works__block">
        <p class="s-recent-works__type">{{ v.type }}</p>
        <h3 class="s-recent-works__title">
          <span v-for="(t, i) in v.title" :key="i">{{ t }}</span>
        </h3>

        <p ref="textRef">{{ v.text }}</p>

        <!-- button  -->
      </div>

      <div class="s-recent-works__block">
        <img :src="v.img" :alt="v.imgAlt" />
      </div>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "vue";

const DATA = [
  {
    id: 1,
    img: "/works/dron.jpeg",
    imgAlt: "dron",
    title: ["Bushwick selfies", "pork belly lyft", "brooklyn messeng"],
    type: "Commercial",
    text: "Narwhal pop-up intelligentsia tbh pinterest, microdosing tilde cloud bread gochujang tattooed leggings cornhole 8-bit. Austin fam chia cold-pressed raw denim. Glossier drinking vinegar portland lo-fi, polaroid bespoke lomo. Banjo art party XOXO, fashion axe sustainable retro ethical gentrify.",
  },
  {
    id: 2,
    img: "/works/audio.jpg",
    imgAlt: "cassette",
    title: ["tumeric tumblr", "gluten-free", "Man bun small"],
    type: "Graphic Design",
    text: "Slow-carb green juice subway tile bicycle rights, fanny pack raclette palo santo put a bird on it mustache actually fam mumblecore iPhone. Iceland post-ironic health goth snackwave, mixtape synth four dollar toast sartorial. Health goth la croix vexillologist, before they sold out shabby chic.",
  },
  {
    id: 3,
    img: "/works/column.jpg",
    imgAlt: "column",
    title: ["batch kombucha", "subway tile", "salvia brooklyn"],
    type: "Branding",
    text: "Mlkshk YOLO wolf, leggings vinyl crucifix stumptown tousled. Pabst venmo gentrify deep v microdosing migas occupy master cleanse intelligentsia sartorial chia activated charcoal. Iceland small batch live-edge raclette roof party dreamcatcher austin pickled. Chillwave cronut messenger bag truffaut.",
  },
  {
    id: 4,
    img: "/works/chocolate.jpg",
    imgAlt: "ice-cream",
    title: ["organic activated", "charcoal vape", "viral ennui"],
    type: "Web design",
    text: "Tote bag cornhole pork belly swag, cronut hoodie snackwave 90's messenger bag pour-over disrupt chartreuse. Vape ugh cardigan hell of. Vaporware umami master cleanse neutra, chartreuse flexitarian lo-fi selvage hella hoodie freegan gentrify. 8-bit air plant umami asymmetrical franzen semiotics before.",
  },
];
export default {
  setup() {
    const workRef = ref([]);
    const textRef = ref([]);
    const titleRef = ref([]);

    const worksObserver = new IntersectionObserver(
      function (entries) {
        entries[0].target.classList.add("active");
      },
      {
        root: null,
        rootMargin: "0px",
        threshold: 0.2,
      }
    );

    const titleObserver = new IntersectionObserver(
      function (entries) {
        entries[0].target.classList.add("active");
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
    };
  },
};
</script>

<style lang="scss" scoped>
.s-recent-works {
  text-align: center;

  &__work {
    display: flex;
    height: 415px; //понять откуда это число
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

  &__main-title {
    @include coveredText($dark-color);

    h2 {
      font-size: 50px;
      line-height: 55px;
      font-weight: 600;
      // color: $dark-color;
      text-transform: uppercase;
      margin: 0;
    }

    @include BlockCoveringText(#fff, 0.5s, 0s);
  }

  &__subtitle {
    opacity: 0;
    transition: opacity 0.5s ease-in 0.3s;

    position: relative;
  }

  &__type {
    @include coveredText($accent-color);

    @include BlockCoveringText($accent-color, 0.5s, 0s);
  }

  &__main-title.active {
    &::after {
      transform: translate3d(100%, 0, 0);
    }

    & + .s-recent-works__subtitle {
      opacity: 1;
    }
  }

  &__title {
    display: flex;
    flex-direction: column;

    span {
      margin: 8px 0;
      align-self: flex-start;
      letter-spacing: 1px;
      @include coveredText($dark-color);

      @include BlockCoveringText($dark-color, 0.3s, 0s);
    }

    span:nth-child(2) {
      @include BlockCoveringText($dark-color, 0.2s, 0.1s);
    }

    span:nth-child(2) {
      @include BlockCoveringText($dark-color, 0.3s, 0.2s);
    }
  }
}

.s-recent-works__work.active {
  .s-recent-works__type,
  .s-recent-works__title span {
    &::after {
      transform: translate3d(100%, 0, 0);
    }
  }

  // .s-recent-works__title {
  //   span {
  //     &::after {
  //       transform: translate3d(100%, 0, 0);
  //     }
  //   }

  //   span:nth-child(2) {
  //     transition-delay: 0.2s;
  //   }

  //   span:nth-child(3) {
  //     transition-delay: 0.6s;
  //   }
  // }
}
</style>
