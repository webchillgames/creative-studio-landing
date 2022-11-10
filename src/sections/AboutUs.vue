<template>
  <div class="s-about-us">
    <div v-for="v in data.titles" :key="v.id">
      {{ v.text }}
    </div>

    <p v-for="v in data.paragraphs" :key="v.id" class="s-about-us__paragraph">
      {{ v.text }}
    </p>

    <p>{{ data.message }}</p>
  </div>
</template>

<script>
const data = {
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

  message: "Godard slow-carb chartreuse occupy, tumblr letterpress",
};
export default {
  setup() {
    return {
      data,
    };
  },
};
</script>

<style lang="scss">
.s-about-us {
  background-color: #000;

  &__paragraph {
    color: #fff;
  }
}
</style>
