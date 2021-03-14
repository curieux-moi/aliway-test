<template>
  <div class="influencer-list">
    <!-- template here cuz we don't want to create useless DOM element -->
    <template v-for="influencer in influencers">
      <influencer
        :key="influencer.id"
        :influencer="influencer"
      />
      <hr :key="influencer.name">
    </template>
  </div>
</template>

<script>
import Influencer from './Influencer.vue'

export default {
  components: { Influencer },
  props: {
    influencers: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
