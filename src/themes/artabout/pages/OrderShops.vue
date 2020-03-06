<template>
  <div id="service-map">
    <div>
      <no-ssr>
        <gmap-map
          ref="map"
          :center="center"
          :options="mapOptions"
          :zoom="14"
          style="width:100%;  height: 91vh;"
        >
          <no-ssr>
            <gmap-marker
              :icon="icon"
              :position="markers[0].position"
              :clickable="true"
              @click="center = markers[0].position"
            />
          </no-ssr>
          <no-ssr>
            <gmap-marker
              :icon="icon"
              :position="markers[1].position"
              :clickable="true"
              @click="center = markers[1].position"
            />
          </no-ssr>
          <gmap-marker
            :key="index"
            v-for="(m, index) in markers"
            :position="m.position"
            :clickable="true"
            @click="center = m.position"
          />
          <no-ssr>
            <gmap-polygon
              ref="polygon"
              :paths="storeKentro"
              :options="pollygonKentroOptions"
              :editable="false"
            />
          </no-ssr>
          <no-ssr>
            <gmap-polygon
              ref="polygon"
              :paths="storeNeapoli"
              :options="pollygonNeapoliOptions"
              :editable="false"
            />
          </no-ssr>
        </gmap-map>
      </no-ssr>
      <div id="service-availability">
        <div id="availability-info" class="align-center">
          <div v-if="this.isAvailable" id="available">
            <h4>Τα καταστήματα μας, εξυπηρετούν στην περιοχή σας.</h4>
          </div>
          <div v-if="!this.isAvailable" id="not-available">
            <h4>Τα καταστήματα μας δεν εξυπηρετούν στην περιοχή σας.</h4>
          </div>
        </div>
      </div>
      <div id="bottom-controls">
        <router-link
          class="back-button p-3 flex center-xs center-md center-lg cl-white brdr-none no-outline pointer align-center mr10"
          :to="localizedRoute('/order')"
          exact
        >
          <i class="material-icons">arrow_back</i>
        </router-link>
        <router-link
          v-if="this.isAvailable"
          class="forward-button flex center-xs center-md center-lg cl-white bg-cl-xred brdr-none no-outline pointer align-center"
          :to="this.theStore + '/sandwich/-3'"
          exact
        >
          <span class="h3 flex center middle-xs ">ΣΥΝΕΧΕΙΑ</span>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import * as VueGoogleMaps from '../../../../node_modules/vue2-google-maps';
import { initCacheStorage } from '@vue-storefront/core/lib/storage-manager';
import { gmapApi } from '../../../../node_modules/vue2-google-maps';
import NoSSR from 'vue-no-ssr';

const storage = initCacheStorage('locationStorage', true);
const availabilityStorage = initCacheStorage('available', true);
const storeStorage = initCacheStorage('availableStore', true);

export default {
  computed: {
    google: gmapApi
  },
  components: {
    'no-ssr': NoSSR
  },
  data () {
    return {
      isAvailable: false,
      theStore: '',
      icon: {
        url: '/assets/large-point.png'
      },
      mapOptions: {
        googleMapsInitialized: false,
        disableDefaultUI: true
      },
      pollygonKentroOptions: {
        fillColor: '#d9251b',
        strokeColor: '#d9251b',
        labelOrigin: { x: 0, y: -100 }
      },
      pollygonNeapoliOptions: {
        fillColor: '#edc56f',
        strokeColor: '#edc56f',
        labelOrigin: { x: 0, y: -100 }
      },
      storeNeapoli: [
        [
          { lng: 22.915249, lat: 40.651178 },
          { lng: 22.907438, lat: 40.654304 },
          { lng: 22.904606, lat: 40.655476 },
          { lng: 22.903576, lat: 40.656453 },
          { lng: 22.908726, lat: 40.659773 },
          { lng: 22.913361, lat: 40.660392 },
          { lng: 22.920613, lat: 40.660945 },
          { lng: 22.926536, lat: 40.661629 },
          { lng: 22.92984, lat: 40.66521 },
          { lng: 22.930698, lat: 40.666121 },
          { lng: 22.932243, lat: 40.666447 },
          { lng: 22.934175, lat: 40.672989 },
          { lng: 22.936578, lat: 40.676733 },
          { lng: 22.939281, lat: 40.677123 },
          { lng: 22.942715, lat: 40.678425 },
          { lng: 22.945933, lat: 40.677644 },
          { lng: 22.947693, lat: 40.672697 },
          { lng: 22.947435, lat: 40.670288 },
          { lng: 22.953959, lat: 40.668009 },
          { lng: 22.963743, lat: 40.665112 },
          { lng: 22.967219, lat: 40.661499 },
          { lng: 22.96782, lat: 40.659285 },
          { lng: 22.961769, lat: 40.655509 },
          { lng: 22.961512, lat: 40.654239 },
          { lng: 22.960997, lat: 40.652611 },
          { lng: 22.960696, lat: 40.650625 },
          { lng: 22.9634, lat: 40.648866 },
          { lng: 22.964945, lat: 40.647564 },
          { lng: 22.966747, lat: 40.644243 },
          { lng: 22.9634, lat: 40.643917 },
          { lng: 22.962284, lat: 40.644764 },
          { lng: 22.959709, lat: 40.644471 },
          { lng: 22.955976, lat: 40.644015 },
          { lng: 22.954903, lat: 40.643461 },
          { lng: 22.952843, lat: 40.643787 },
          { lng: 22.951427, lat: 40.644927 },
          { lng: 22.949581, lat: 40.644145 },
          { lng: 22.948594, lat: 40.644178 },
          { lng: 22.94486, lat: 40.64535 },
          { lng: 22.943187, lat: 40.644438 },
          { lng: 22.941813, lat: 40.64395 },
          { lng: 22.935419, lat: 40.640791 },
          { lng: 22.915249, lat: 40.651178 }
        ]
      ],
      storeKentro: [
        [
          { lng: 22.941599, lat: 40.644015 },
          { lng: 22.944732, lat: 40.645057 },
          { lng: 22.949281, lat: 40.643885 },
          { lng: 22.951255, lat: 40.644992 },
          { lng: 22.954988, lat: 40.643461 },
          { lng: 22.957864, lat: 40.644373 },
          { lng: 22.961855, lat: 40.644764 },
          { lng: 22.963743, lat: 40.643657 },
          { lng: 22.966576, lat: 40.643559 },
          { lng: 22.96546, lat: 40.641735 },
          { lng: 22.963958, lat: 40.640758 },
          { lng: 22.96267, lat: 40.639912 },
          { lng: 22.964087, lat: 40.639228 },
          { lng: 22.963657, lat: 40.638121 },
          { lng: 22.968163, lat: 40.633854 },
          { lng: 22.968936, lat: 40.633301 },
          { lng: 22.969322, lat: 40.629946 },
          { lng: 22.968421, lat: 40.62949 },
          { lng: 22.969108, lat: 40.628611 },
          { lng: 22.969966, lat: 40.626363 },
          { lng: 22.970266, lat: 40.625972 },
          { lng: 22.971854, lat: 40.625386 },
          { lng: 22.973356, lat: 40.625158 },
          { lng: 22.976317, lat: 40.6248 },
          { lng: 22.977948, lat: 40.62353 },
          { lng: 22.97606, lat: 40.621184 },
          { lng: 22.973828, lat: 40.620728 },
          { lng: 22.971168, lat: 40.620305 },
          { lng: 22.970867, lat: 40.619784 },
          { lng: 22.968636, lat: 40.618937 },
          { lng: 22.967477, lat: 40.617699 },
          { lng: 22.969837, lat: 40.614246 },
          { lng: 22.971511, lat: 40.609424 },
          { lng: 22.963099, lat: 40.607502 },
          { lng: 22.961254, lat: 40.607111 },
          { lng: 22.957778, lat: 40.607111 },
          { lng: 22.950354, lat: 40.60685 },
          { lng: 22.950954, lat: 40.613855 },
          { lng: 22.951727, lat: 40.619067 },
          { lng: 22.951941, lat: 40.621249 },
          { lng: 22.950997, lat: 40.623139 },
          { lng: 22.947993, lat: 40.625321 },
          { lng: 22.94735, lat: 40.627178 },
          { lng: 22.937436, lat: 40.633594 },
          { lng: 22.934818, lat: 40.631444 },
          { lng: 22.934132, lat: 40.631998 },
          { lng: 22.935634, lat: 40.633268 },
          { lng: 22.932243, lat: 40.635711 },
          { lng: 22.925978, lat: 40.638283 },
          { lng: 22.914391, lat: 40.640726 },
          { lng: 22.905464, lat: 40.644243 },
          { lng: 22.909198, lat: 40.649029 },
          { lng: 22.911644, lat: 40.652448 },
          { lng: 22.934775, lat: 40.640693 },
          { lng: 22.93499, lat: 40.640726 },
          { lng: 22.941599, lat: 40.644015 }
        ]
      ],
      center: {
        lat: parseFloat(this.lat),
        lng: parseFloat(this.lng)
      },
      markers: [
        { position: { lat: 40.631829, lng: 22.944388 } },
        { position: { lat: 40.650579, lng: 22.938524 } }
      ]
    };
  },
  beforeMount () {
    this.getLocation();
    this.addMarker();
  },
  mounted () {
    this.$nextTick(() => {
      this.$refs.map.$mapPromise.then(() => {
        this.googleMapsInitialized = true;
        setTimeout(() => {
          this.test();
          this.getStore();
          this.isStoreAvailable();
        }, 200);
      });
    });
  },
  methods: {
    async getStore () {
      const store = await storeStorage.getItem('store');
      if (store === 'neapoli') this.theStore = store;
    },
    async isStoreAvailable () {
      const sa = await availabilityStorage.getItem('isAvailable');
      this.isAvailable = sa;
    },
    test () {
      console.log(this.$refs.map);
      if (!this.googleMapsInitialized) return null;

      // eslint-disable-next-line no-undef
      var shopKentroPolygon = new google.maps.Polygon({
        paths: this.storeKentro,
        map: this.$refs.map
      });
      // eslint-disable-next-line no-undef
      var shopNeapoliPolygon = new google.maps.Polygon({
        paths: this.storeNeapoli,
        map: this.$refs.map
      });

      // eslint-disable-next-line no-undef
      let curPosition = new google.maps.LatLng(
        this.center.lat,
        this.center.lng
      );

      // eslint-disable-next-line no-undef
      let resultShopKentro = !!google.maps.geometry.poly.containsLocation(
        curPosition,
        shopKentroPolygon
      );
      // eslint-disable-next-line no-undef
      let resultShopNeapoli = !!google.maps.geometry.poly.containsLocation(
        curPosition,
        shopNeapoliPolygon
      );

      if (resultShopKentro) {
        this.availability = true;
        availabilityStorage.setItem('isAvailable', true);
        storeStorage.setItem('store', 'kentro');
      } else if (resultShopNeapoli) {
        this.availability = true;
        availabilityStorage.setItem('isAvailable', true);
        storeStorage.setItem('store', 'neapoli');
      } else {
        this.availability = false;
        availabilityStorage.setItem('isAvailable', false);
      }
      // google.maps.event.addDomListener(window, 'load', initMap);

      // var b = new google.maps.LatLngBounds();
      // console.log(s);
      // b.extend(this.paths);

      // console.log(b);
      // var bounds = this.$refs.map.$mapObject.getBounds()
      //   console.log(b.getCenter().lng())
      // this.$refs.polygon.paths[0].forEach(element => {
      //   console.log(element.lat);
      //   console.log(element.lng);
      // });
      // console.log(this.$refs.polygon.paths[0][0].lat)
    },
    geolocate: function () {
      navigator.geolocation.getCurrentPosition(position => {
        this.center = {
          lat: position.coords.latitude,
          lng: position.coords.longitude
        };
        this.addMarker();
      });
    },
    async addMarker () {
      const lat = await storage.getItem('lat');
      const lng = await storage.getItem('lng');
      const marker = {
        lat: parseFloat(lat),
        lng: parseFloat(lng)
      };
      this.markers.push({ position: marker });
    },
    async getLocation () {
      const lat = await storage.getItem('lat');
      const lng = await storage.getItem('lng');
      if (lat && lng) {
        this.center.lat = lat;
        this.center.lng = lng;
      } else {
        this.center.lat = 46.1254;
        this.center.lng = 41.15487;
      }
    }
  },
  metaInfo () {
    return {
      title: this.$route.meta.title || this.$props.title,
      meta: this.$route.meta.description
        ? [{ vmid: 'description', description: this.$route.meta.description }]
        : []
    };
  }
};
</script>

<style lang="scss" scoped>
footer {
  display: none;
}
#service-availability {
  position: fixed;
  top: 15vh;
  left: calc(-50% + 50vw);
  width: 100vw;
  text-align: center;
}
#not-available {
  animation: fadein 2s;
  width: 300px;
  margin: auto;
  padding: 0.5em;
  background-color: #d9251ba1;
  border-radius: 10px;

  h4,
  p {
    color: white;
  }
}

#available {
  animation: fadein 2s;
  width: 300px;
  margin: auto;
  padding: 0.5em;
  background-color: #1cb61ca1;
  border-radius: 10px;

  h4,
  p {
    color: white;
  }
}
@keyframes fadein {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
#bottom-controls {
  position: fixed;
  display: flex;
  justify-content: center;
  width: 100vw;
  margin: 0 auto;
  left: calc(-50% + 50vw);
  bottom: 5vh;
  .back-button {
    background-color: rgba(0, 0, 0, 0.4);
    border-radius: 3px;
    width: 70px;
    align-items: center;
  }
  .material-icons {
    font-size: 44px;
    color: white;
  }
  .forward-button {
    background-color: #d9251b;
    border-radius: 3px;
    color: white;
    text-shadow: 0 0 2px rgba(0, 0, 0, 0.596);
    width: 300px;
  }
  @media (max-width: 425px) {
    .forward-button {
      width: 65vw;
    }
  }
}
</style>
