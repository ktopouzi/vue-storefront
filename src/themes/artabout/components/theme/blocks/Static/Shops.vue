<template>
  <div class="row">
    <div class="col-md-6">
      <div class="kentro-wrapper center-xs p10">
        <img width="100%" src="/assets/Xristos-katastima-kentrou.jpg" alt="">
        <div class="shop-name bg-cl-xred cl-white w-90 m-auto">
          <h4 class="bold m0 p0">
            Κατάστημα Κέντρου
          </h4>
          <p class="m0 p0">
            Εγνατίας 150
          </p>
        </div>
        <div class="shop-info my20 brdr-bottom-1 brdr-cl-xgray">
          <h4 class="bold m0 p0">
            ΩΡΑΡΙΟ ΚΑΤΑΣΤΗΜΑΤΟΣ
          </h4>
          <p class="m0 mb20 p0 cl-xgray">
            10:00 πμ - 04:00 πμ
          </p>
        </div>
        <div class="shop-info my20 brdr-bottom-1 brdr-cl-xgray">
          <h4 class="bold m0 p0">
            DELIVERY
          </h4>
          <p class="m0 mb20 p0 cl-xgray">
            11:00 πμ - 03:30 πμ
          </p>
        </div>
        <div class="shop-info my20">
          <h4 class="bold m0 p0">
            Τηλέφωνα
          </h4>
          <p class="m0 p0 cl-xgray">
            Tηλ. <span class="til cl-xred">2310.254.466</span>
          </p>
          <p class="m0 p0 cl-xgray">
            Tηλ. <span class="til cl-xred">2310.254.469</span>
          </p>
          <p class="m0 p0 cl-xgray">
            Whats Up: <span class="til cl-xred">6987.233.673</span>
          </p>
          <p class="m0 mb20 p0 cl-xgray">
            Vodafone : <span class="til cl-xred">6940.704.911</span>
          </p>
        </div>
        <div class="shop-map">
          <no-ssr>
            <gmap-map
              ref="map"
              :center="markers[0].position"
              :options="mapOptions"
              :zoom="16"
              style="width:100%;  height: 40vh;"
            >
              <no-ssr>
                <gmap-marker
                  :icon="{ url: require('../../../../assets/large-point.png')}"
                  :position="markers[0].position"
                  :clickable="true"
                  @click="center = markers[0].position"
                />
              </no-ssr>
            </gmap-map>
          </no-ssr>
        </div>
      </div>
    </div>
    <div class="col-md-6">
      <div class="neapoli-wrapper center-xs p10">
        <img width="100%" src="/assets/Xristos-katastima-neapolis.jpg" alt="">
        <div class="shop-name bg-cl-xred cl-white w-90 m-auto">
          <h4 class="bold m0 p0">
            Κατάστημα Νεαπόλεως
          </h4>
          <p class="m0 p0">
            Ελευθερίου Βενιζέλου 56-58
          </p>
        </div>
        <div class="shop-info my20 brdr-bottom-1 brdr-cl-xgray">
          <h4 class="bold m0 p0">
            ΩΡΑΡΙΟ ΚΑΤΑΣΤΗΜΑΤΟΣ
          </h4>
          <p class="m0 mb20 p0 cl-xgray">
            10:00 πμ - 04:00 πμ
          </p>
        </div>
        <div class="shop-info my20 brdr-bottom-1 brdr-cl-xgray">
          <h4 class="bold m0 p0">
            DELIVERY
          </h4>
          <p class="m0 mb20 p0 cl-xgray">
            11:00 πμ - 03:30 πμ
          </p>
        </div>
        <div class="shop-info my20">
          <h4 class="bold m0 p0">
            Τηλέφωνα
          </h4>
          <p class="m0 p0 cl-xgray">
            Tηλ. <span class="til cl-xred">2310.633.183</span>
          </p>
          <p class="m0 p0 cl-xgray">
            Tηλ. <span class="til cl-xred">2310.633.185</span>
          </p>
          <p class="m0 p0 cl-xgray">
            Whats Up: <span class="til cl-xred">6971.501.591</span>
          </p>
          <p class="m0 mb20 p0 cl-xgray">
            Vodafone : <span class="til cl-xred">6940.706.073</span>
          </p>
        </div>
        <div class="shop-map">
          <no-ssr>
            <gmap-map
              ref="map"
              :center="markers[1].position"
              :options="mapOptions"
              :zoom="16"
              style="width:100%;  height: 40vh;"
            >
              <no-ssr>
                <gmap-marker
                  :icon="{ url: require('../../../../assets/large-point.png')}"
                  :position="markers[1].position"
                  :clickable="true"
                  @click="center = markers[1].position"
                />
              </no-ssr>
            </gmap-map>
          </no-ssr>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import * as VueGoogleMaps from '@vue-storefront/../../node_modules/vue2-google-maps';
import NoSSR from 'vue-no-ssr';
import { gmapApi } from '@vue-storefront/../../node_modules/vue2-google-maps';

export default {
  computed: {
    google: gmapApi
  },
  icon: {
    url: '/assets/large-point.png'
  },
  components: {
    'no-ssr': NoSSR
  },
  data () {
    return {
      mapOptions: {
        googleMapsInitialized: false,
        disableDefaultUI: true
      },
      markers: [
        { position: { lat: 40.631829, lng: 22.944388 } },
        { position: { lat: 40.650579, lng: 22.938524 } }
      ]
    }
  }
}
</script>

<style lang="scss" scoped>
.til {
    font-weight: bold;
}
</style>
