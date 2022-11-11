<template>
  <div class="s-our-clients" ref="sectionRef">
    <div class="container small">
      <CColoringTitle :text="DATA.title" />

      <ul class="brands">
        <li v-for="v in DATA.companies" :key="v.id" class="brand">
          <div class="brand__wrapper">
            <img :src="v.img" class="brand__img" />
            <img :src="v.imgAccent" class="brand__hover-img" />
          </div>
        </li>
        <li class="brands__free-spot brand">
          <CColoringTitle :text="['this spot', 'awaits', 'you']" />
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import CColoringTitle from "@/components/CColoringTitle.vue";
import { OUR_CLIENTS as DATA } from "@/data.js";
import { onMounted, ref } from "vue";

export default {
  components: { CColoringTitle },
  setup() {
    const sectionRef = ref({});

    const observer = new IntersectionObserver(
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
      observer.observe(sectionRef.value);
    });

    return {
      sectionRef,
      CColoringTitle,
      DATA,
    };
  },
};
</script>

<style lang="scss">
.s-our-clients {
  background-color: #1b2a2f;
  padding: 120px 20px;
}

.brands {
  display: flex;
  flex-wrap: wrap;

  .brand {
    flex-basis: 25%;
    text-align: center;
    height: 220px;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: none;
    border-bottom: 1px solid #888888;
    box-sizing: border-box;
    border-right: 1px solid #888888;
    position: relative;
    cursor: pointer;
    list-style: none;

    &__wrapper {
      width: 150px;
      height: 150px;
      position: relative;

      img {
        width: 100%;
        height: 100%;
      }
    }

    .brand__hover-img {
      position: absolute;
      top: 0;
      left: 0;
      opacity: 0;
      transition: opacity 0.1s ease-in;
    }

    &:hover {
      .brand__hover-img {
        opacity: 1;
      }
    }
  }

  li:nth-child(4n) {
    border-right: none;
  }

  li:nth-last-child(1),
  li:nth-last-child(2),
  li:nth-last-child(3),
  li:nth-last-child(4) {
    border-bottom: none;
  }

  &__free-spot {
    position: relative;
  }
}

.s-our-clients.active {
  .c-coloring-title span::after {
    transform: translate3d(110%, 0, 0);
  }
}
</style>
