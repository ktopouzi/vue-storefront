<template>
  <div class="breadcrumbs h5 cl-white">
    <span class="cl-white" v-for="link in paths" :key="link.route_link">
      <router-link class="cl-white" :to="link.route_link">
        {{ link.name | htmlDecode }}
      </router-link> /
    </span>
    <span class="cl-white">
      {{ current | htmlDecode }}
    </span>
  </div>
</template>

<script>
import { Breadcrumbs } from '@vue-storefront/core/modules/breadcrumbs/components/Breadcrumbs.ts'

export default {
  mixins: [Breadcrumbs]
}
</script>
