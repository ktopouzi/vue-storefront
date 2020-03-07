<template>
  <div id="order-now">
    <div class="container">
      <div class="row align-center info-row">
        <div class="col-xs-12 col-sm-12 col-md-12">
          <div class="align-center cl-white pt40">
            <img src="../assets/marker-pin.png" alt="gooogle map marker pin in red colour">
            <h2>ΒΑΛΕ ΤΗ ΔΙΕΥΘΥΝΣΗ ΣΟΥ</h2>
            <hr class="brdr-none no-outline bg-cl-xred orderhr">
          </div>
        </div>
      </div>
      <div class="row align-center pt50">
        <div class="col-xs-12 col-sm-12 col-md-12">
          <div class="align-center cl-white">
            <no-ssr>
              <gmap-autocomplete
                id="autocomplete"
                class="p10 cl-black"
                placeholder="πχ. Γιαννιτσών 90"
                :select-first-on-enter="true"
                @place_changed="setPlace"
                :options="autocompleteOptions"
              />
            </no-ssr>
          </div>
          <img class="pt50" width="200px" src="../assets/order-xristos-logo.png" alt="xristos logo">
        </div>
      </div>
      <div class="row align-center pt50">
        <div class="col-xs-12 col-sm-12 col-md-12">
          <router-link
            class="flex center-xs p25 cl-white bg-cl-xred brdr-none no-outline pointer align-center order-now-btn"
            :to="localizedRoute('/katastimata')"
            exact
          >
            ΣΥΝΕΧΕΙΑ
          </router-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { isServer, onlineHelper } from '@vue-storefront/core/helpers';
import NoSSR from 'vue-no-ssr';
import * as VueGoogleMaps from '../../../../node_modules/vue2-google-maps';
import { initCacheStorage } from '@vue-storefront/core/lib/storage-manager';

export default {
  data () {
    return {
      currentPlace: null,
      autocompleteOptions: {
        bounds: {
          north: 40.6560448,
          south: 40.5863402,
          east: 22.99007119999999,
          west: 22.901983299999984
        },
        componentRestrictions: { country: 'gr' }
      }
    };
  },
  mounted () {},
  computed: {},
  metaInfo () {
    return {
      title: this.$route.meta.title || this.$props.title,
      meta: this.$route.meta.description
        ? [{ vmid: 'description', description: this.$route.meta.description }]
        : []
    };
  },
  components: {
    'no-ssr': NoSSR
  },
  methods: {
    // receives a place object via the autocomplete component
    async setPlace (place) {
      this.currentPlace = place;
      const storage = initCacheStorage('locationStorage', true);
      const lng = await storage.getItem('lng');
      const lat = await storage.getItem('lat');
      storage.setItem('lat', this.currentPlace.geometry.location.lat());
      storage.setItem('lng', this.currentPlace.geometry.location.lng());
    }
  }
};
</script>

<style lang="scss" scoped>
.pac-container:after {
  display: none;
}

#autocomplete {
  width: 90%;
  max-width: 420px;
  font-family: "Gotham Greek Book";
}
#order-now {
  height: 100%;
  background: url("/assets/wood_bg.jpg");
  background-position-y: center;
  padding-bottom: 90px;

  img {
    margin: auto;
  }
}

.info-row {
  h2 {
    font-family: "Gotham Greek Book";
    font-weight: 100;
  }
}
.orderhr {
  border: none;
  margin: 10px auto;
  width: 190px;
  height: 2px;
  outline: none;
}
.order-now-btn {
  margin: auto;
  max-width: 280px;
  font-size: 20px;
  text-shadow: 0 0 4px #00000059;
  &:hover,
  &:focus {
    border: none;
  }
  &:after {
    display: none;
  }
}
</style>
