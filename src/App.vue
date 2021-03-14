<template>
  <div id="app">
    <filter-list
      :filters="filters"
      :total-items="influencers.length"
      @change-sort-type="setActiveFilter"
    />
    <hr>
    <loader v-if="!influencersLoaded" />
    <influencer-list :influencers="sortedInfluencers" v-if="influencersLoaded" />
  </div>
</template>

<script>
import FilterList from './components/FilterList'
import InfluencerList from './components/InfluencerList'
import Loader from './components/Loader.vue'
import FieldService from './FieldService'

const fieldService = new FieldService()

export default {
  name: 'App',
  components: {
    FilterList,
    InfluencerList,
    Loader
  },
  data: () => ({
    influencersLoaded: false,
    filters: [
      {
        id: 1,
        title: 'Подписчиков',
        value: 'followers'
      },
      {
        id: 2,
        title: 'Рейтинг увлеченности',
        value: 'er'
      }
    ],
    sortBy: {},
    influencers: []
  }),
  methods: {
    setActiveFilter (filter) {
      const filterFound = this.filters.find(f => f.id === filter.id)
      if (filterFound) {
        this.sortBy = { field: filterFound.value, ascending: filter.active }
      }
    }
  },
  computed: {
    sortedInfluencers () {
      if (!this.sortBy.field) return this.influencers
      return [...this.influencers].sort((a, b) => {
        const left = a[this.sortBy.field]
        const right = b[this.sortBy.field]
        if (this.sortBy.ascending) {
          return left - right
        }
        return right - left
      })
    }
  },
  async created () {
    this.influencers = await fieldService.getInfluencers()
    this.influencersLoaded = true
  }
}
</script>

<style lang="scss">
#app {
  padding: 0 50px;
  font-family: 'Open Sans', sans-serif;
  font-size: 16px;
  color: #2c3e50;
}
</style>
