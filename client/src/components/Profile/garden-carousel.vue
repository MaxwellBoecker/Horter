<template>
  <div class="ui segment">
    <div class="ui grid container" :user0="user0">
      <carousel-3d>
        <div class="ui segment" v-for="(garden, i) in user0.gardens" :key="i">
          <slide :index="i">
            {{ garden.name }}
            <img :src="garden.photo" />
          </slide>
        </div>
      </carousel-3d>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
import carousel3d from "vue-carousel-3d";
import user0 from "./user-profile.vue";
import { Carousel3d, Slide } from "vue-carousel-3d";

Vue.use(Carousel3d);

export default {
  name: "Carousel",

  components: {
    Carousel3d,
    Slide,
  },
  props: ["user0"],

  data() {
    return {
      // user0: user0,
    };
  },

  methods: {
    getGardens: () => {
      axios
        .post(`/garden${this.user.id}`, {
          plantId: treflePlantId,
          slug: treflePlantSlug,
          gardenId: this.gardenId,
        })
        .then((res) => {
          this.$log.info(res);
        })
        .catch((err) => {
          console.error(err);
        });
      this.keyword = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.is-active .al img {
  border: 1px solid #fff;
  filter: grayscale(0%);
}
.al img {
  border: 1px solid transparent;
  filter: grayscale(100%);
}
</style>
