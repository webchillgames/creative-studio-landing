<template>
  <div class="s-about-us">
    <div class="s-about-us__titles">
      <div
        v-for="v in DATA.titles"
        :key="v.id"
        class="s-about-us__title"
        :data-text="v.text"
      >
        {{ v.text }}
      </div>
    </div>

    <div class="s-about-us__paragraphs">
      <p v-for="v in DATA.paragraphs" :key="v.id">
        {{ v.text }}
      </p>
    </div>

    <p class="s-about-us__message">{{ DATA.message }}</p>
  </div>
</template>

<script>
const DATA = {
  message: "Godard slow-carb chartreuse occupy, tumblr letterpress",
  titles: [
    { id: 1, text: "We are Creative" },
    { id: 2, text: "We are Xen" },
  ],

  paragraphs: [
    {
      id: 1,
      text: "Affogato thundercats quinoa, portland cold-pressed edison bulb artisan paleo banjo tousled try-hard food truck pop-up bushwick godard. Occupy 90s try-hard tote bag chicharrones stumptown polaroid hashtag cliche +1, tousled fanny pack. Tote bag iPhone crucifix hella helvetica food truck bicycle rights cloud bread. Yr iPhone asymmetrical, next level vexillologist godard blog green juice chia. Tacos jean shorts pickled PBR&B poutine.",
    },
    {
      id: 2,
      text: "Godard slow-carb chartreuse occupy, tumblr letterpress pok pok tattooed yr lyft yuccie kinfolk. IPhone kombucha shaman gastropub snackwave 90's lo-fi pug chillwave pok pok tofu. Swag deep v listicle roof party seitan man braid raclette church-key trust fund locavore vexillologist green juice raw denim tilde meh. Austin thundercats locavore taiyaki snackwave hoodie put a bird on it tattooed selvage kitsch ramps. ",
    },
  ],
};
export default {
  setup() {
    return {
      DATA,
    };
  },
};
</script>

<style lang="scss">
.s-about-us {
  padding: 120px 20px;
  background-color: #000;

  &__paragraphs {
    display: flex;

    p {
      color: #fff;
      font-size: 16px;
      line-height: 1.8;
      font-weight: 600;
      letter-spacing: 0px;
      font-family: "Open Sans", sans-serif;
    }

    p + p {
      margin-left: 30px;
    }
  }

  &__message {
    margin: 0;
    margin-top: 60px;
    color: #fff;
    text-align: center;
    font-weight: 400;
    letter-spacing: 5px;
    font-family: "Oswald", sans-serif;
  }

  &__title {
    text-transform: uppercase;
    position: relative;
    font-size: 50px;
    font-weight: 600;
    font-family: "Oswald", sans-serif;

    &::after {
      color: $accent-color;
      animation: coloring 1s ease-out 0s infinite;
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

@keyframes coloring {
  0% {
    width: 0;
    // transform: scale(0) translate3d(-100%, 0, 0);
  }

  100% {
    width: 100%;
    // transform: scale(1) translate3d(0, 0, 0);
  }
}
</style>
