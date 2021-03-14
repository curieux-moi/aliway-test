<template>
  <div class="filter-list">
    <span>Всего найдено: {{ totalItems }}</span>
    <filter-list-item
      v-for="filter in filters"
      :key="filter.id"
      :filter="filter"
      :active="activeFilter.id === filter.id"
      @click.native="setActiveFilter(filter)"
    />
  </div>
</template>

<script>
import FilterListItem from './FilterListItem.vue'

export default {
  components: {
    FilterListItem
  },
  props: {
    filters: {
      type: Array,
      default: () => []
    },
    totalItems: {
      type: Number,
      default: 0
    }
  },
  data: () => ({
    activeFilter: {}
  }),
  methods: {
    setActiveFilter (filter) {
      let active = true
      if (this.activeFilter.id === filter.id) {
        this.activeFilter = {}
        active = false
      } else {
        this.activeFilter = filter
      }

      this.$emit('change-sort-type', {
        ...filter,
        active
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.filter-list {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
</style>
