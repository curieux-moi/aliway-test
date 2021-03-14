<template>
  <a class="influencer" :href="influencer.profileUrl">
    <div class="influencer__info">
      <img :src="influencer.avatarUrl" alt="user avatar" class="avatar">
      <span>@{{ influencer.name }}</span>
      <span>{{ influencer.fullName }}</span>
    </div>
    <span>{{ influencer.followers }}</span>
    <span>{{ influencer.er }}%</span>
  </a>
</template>

<script>
export default {
  props: {
    influencer: {
      type: Object,
      default: () => ({})
    }
  }
}
</script>

<style lang="scss" scoped>
.avatar {
  width: 150px;
  border-radius: 50%;
}

.influencer {
  padding: 25px 0;
  color: inherit;
  text-decoration: none;

  &:hover {
    background: #d8f3fdab;
  }
}

.influencer, .influencer__info {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  align-items: center;
}
</style>
