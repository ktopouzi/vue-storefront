<template>
  <section class="container px5">
    <no-ssr>
      <carousel
        :per-page-custom="[[480, 3], [768, 5]]"
        :scroll-per-page="false"
        :mouse-drag="true"
        :loop="true"
        :navigation-enabled="false"
        :pagination-enabled="false"
        ref="carousel"
      >
        <slide :key="category.slug" v-for="category in categories">
          <router-link
            class="cl-accent no-underline col-xs slider-link pt5"
            :to="categoryLink(category)"
            style="display:flex; flex-direction:column;align-items: center;"
          >
            <img
              style="mb20"
              height="40px"
              width="40px"
              :src="imagesMap(category.id)"
              alt="category alt"
            >

            <p id="category-slider-text" class="mb0 align-center">
              {{ category.name }}
            </p>
          </router-link>
        </slide>
      </carousel>
    </no-ssr>
    <!-- <hooper :infiniteScroll="true" :itemsToShow="3">
      <slide :key="category.slug" v-for="category in categories">
        <router-link
          class="cl-accent no-underline col-xs slider-link pt5"
          :to="categoryLink(category)"
          style="display:flex; flex-direction:column;align-items: center;"
        >
          <img
            style="mb20"
            height="40px"
            width="40px"
            :src="imagesMap(category.id)"
            alt="category alt"
            @click.prevent="nav(category)"
            @dragstart.prevent="console.log('ha')"
          />

          <p class="mb0 align-center">{{ category.name }}</p>
          <span class="category-brdr"></span>
        </router-link>
      </slide>
      <hooper-navigation class="hidden-xs" slot="hooper-addons"></hooper-navigation>
    </hooper>-->
  </section>
</template>

<script>
// Hooper
// import { Hooper, Slide, Navigation as HooperNavigation } from "hooper";
import { Carousel, Slide } from 'vue-carousel';
import NoSSR from 'vue-no-ssr';
import { formatCategoryLink } from '@vue-storefront/core/modules/url/helpers';

export default {
  components: {
    Carousel,
    Slide,
    'no-ssr': NoSSR
  },
  data () {
    return {
      itemToShow: 4
    };
  },
  computed: {
    categories () {
      return this.$store.state.category.list.filter(c => {
        return c.id !== 2;
      }); // return my child categories;
    }
  },
  methods: {
    imagesMap (id) {
      switch (id) {
        case 3:
          return '../../assets/icons/sandwitch.svg';
        case 4:
          return '../../assets/icons/anapsiktika.svg';
        case 5:
          return '../../assets/icons/burger.svg';
        case 6:
          return '../../assets/icons/merida.svg';
        case 7:
          return '../../assets/icons/temaxia.svg';
        case 8:
          return '../../assets/icons/orektika.svg';
        case 9:
          return '../../assets/icons/squid.svg';
        case 10:
          return '../../assets/icons/salata.svg';
        case 11:
          return '../../assets/icons/alifes.svg';
        case 12:
          return '../../assets/icons/pota.svg';
        default:
          break;
      }
    },
    categoryLink (category) {
      return formatCategoryLink(category);
    }
  }
};
</script>

<style lang="scss" scoped>
.slider-link {
  img {
    height: 40px;
    width: 40px;
  }
}
.slider-link.router-link-active {

#category-slider-text {
  border-bottom: 3px solid #d9251b;
}
  font-weight: bold;
  img {
    filter: invert(0.4) sepia(1) saturate(20) hue-rotate(325.6deg)
      brightness(0.8);
  }
}
</style>
