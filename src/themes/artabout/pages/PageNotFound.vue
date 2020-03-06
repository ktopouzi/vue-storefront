<template>
  <div id="page_not_found">
    <section class="bg-cl-black cl-white py35 px20">
      <div class="container">
        <h2>
          {{ $t("We can't find the page") }}
        </h2>
      </div>
    </section>
    <section class="bg-cl-primary py35 px20">
      <div class="container">
        <div class="lh16 h5 weight-400">
          <p>
            {{ $t("Unfortunately we can't find the page you are looking for.") }}
          </p>
          <p>
            {{ $t('You can also use') }}
            <a href="#" class="cl-secondary no-underline" @click="toggleSearchpanel">
              εδώ
            </a>
          </p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import { Logger } from '@vue-storefront/core/lib/logger'
import i18n from '@vue-storefront/i18n'
import LazyHydrate from 'vue-lazy-hydration'
import ProductTile from '../components/core/ProductTile.vue'

export default {
  name: 'PageNotFound',
  computed: {
    ...mapGetters({
      ourBestsellersCollection: 'homepage/getBestsellers'
    })
  },
  async asyncData ({ store, route, context }) {
    Logger.log('Entering asyncData for PageNotFound ' + new Date())()
    if (context) {
      context.output.cacheTags.add(`page-not-found`)
      context.server.response.statusCode = 404
    }

    await store.dispatch('homepage/loadBestsellers')
  },
  metaInfo () {
    return {
      title: this.$route.meta.title || i18n.t('404 Page Not Found'),
      meta: this.$route.meta.description ? [{ vmid: 'description', name: 'description', content: this.$route.meta.description }] : []
    }
  },
  components: {
    ProductTile,
    LazyHydrate
  },
  methods: {
    toggleSearchpanel () {
      this.$store.commit('ui/setSearchpanel', true)
    }
  }
}
</script>

<style scoped>
  a {
    text-decoration: underline;
  }
</style>
