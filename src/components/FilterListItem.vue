<template>
  <div class="filter-list__item">
    {{ filter.title }}
    <img
      src="../assets/filter-arrow.png"
      alt="filter-arrow"
      :class="['filter-arrow', {'filter-arrow_active': active}]"
    >
  </div>
</template>

<script>
export default {
  props: {
    filter: {
      type: Object,
      default: () => ({})
    },
    active: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped lang="scss">
.filter-list__item {
  display: flex;
  cursor: pointer;
}

.filter-arrow {
  margin-left: 5px;
  width: 20px;

  &_active {
    transform: rotate(180deg);
  }
}
</style>
