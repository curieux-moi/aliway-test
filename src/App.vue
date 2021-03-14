<template>
  <div id="app">
    <filter-list
      :filters="filters"
      :total-items="influencers.length"
      @change-sort-type="setActiveFilter"
    />
    <hr>
    <influencer-list :influencers="sortedInfluencers" />
  </div>
</template>

<script >
import FilterList from './components/FilterList'
import InfluencerList from './components/InfluencerList'
import FieldService from './FieldService'

const fieldService = new FieldService()

export default {
  name: 'App',
  components: {
    FilterList,
    InfluencerList
  },
  data: () => ({
    filters: [
      {
        id: 1,
        title: 'Подписчиков',
        descending: true,
        value: 'followers'
      },
      {
        id: 2,
        title: 'Рейтинг увлеченности',
        descending: true,
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
      // if (filterFound.id === this.activeFilter.id) {
      //   this.activeFilter.sortType === 'desc'
      //     ? this.activeFilter.sortType = 'asc'
      //     : this.activeFilter.sortType = 'desc'
      // } else {
      //   this.activeFilter = { ...filterFound, sortType: 'asc' }
      // }
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
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
