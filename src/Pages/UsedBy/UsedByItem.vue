<template>
  <li class="used-by-item" v-if="user.star > 10">
    <div class="used-by-item__name">
      <div class="used-by-item__name-avatar">
        <img
          class="used-by-item__name-avatar__image"
          :src="user.avatar"
          alt=""
        />
      </div>
      <a
        :href="`https://github.com/${user.name}`"
        class="used-by-item__name-link"
        >{{ user.name }}</a
      >
    </div>
    <div class="used-by-item__star">
      <img
        class="used-by-item__star-image"
        :src="require('@/assets/StarIcon.svg')"
        alt=""
      />
      {{ user.star }}
    </div>
  </li>
</template>

<script>
export default {
  name: "used-by-item",

  props: {
    user: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="sass">
.used-by-item
  width: 100%
  display: flex
  align-items: center
  justify-content: space-between
  background-color: #1c1e21
  padding: 1rem
  border: .125rem solid #323438
  color: #C4C4C4

.used-by-item__name
  display: flex
  align-items: center
  gap: 1rem

.used-by-item__name-link
  text-decoration: none
  color: #c4c4c4

.used-by-item__name-avatar
  max-width: 1.5625rem
  max-height: 1.5625rem

.used-by-item__name-avatar__image
  width: 100%
  height: 100%
  border-radius: 50%
.used-by-item__star
  display: flex
  align-items: center
  gap: .5rem
  &-image
    width: 100%
</style>
