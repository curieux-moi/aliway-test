<template>
  <div :class="['filter-list__item', {'filter-list__item_active': active}]">
    {{ filter.title }}
    <img
      src="../assets/filter-arrow.svg"
      alt="filter-arrow"
      class="filter-arrow"
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

  &_active {
    color: #42b983;

    img {
      filter: invert(61%) sepia(74%) saturate(349%) hue-rotate(101deg) brightness(89%) contrast(83%);
      transform: rotate(180deg);
    }
  }
}

.filter-arrow {
  margin-left: 5px;
  width: 20px;
}
</style>
