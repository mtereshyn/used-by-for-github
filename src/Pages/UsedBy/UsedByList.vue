<template>
  <div class="used-by-list">
    <ul class="used-by-list__list">
      <used-by-item
        v-for="(user, index) in sortedList"
        :key="index"
        :user="user"
      />
    </ul>
  </div>
</template>

<script>
import UsedByItem from "@/Pages/UsedBy/UsedByItem";
export default {
  name: "used-by-list",
  components: {
    UsedByItem,
  },
  props: {
    sortedList: {
      type: Array,
      required: false,
    },
    nextPageLink: {
      type: String,
      required: false,
    },
  },
};
</script>

<style lang="sass">
.used-by-list__list
  list-style: none
  display: flex
  flex-direction: column
  align-items: center
  gap: 1rem
  max-width: 70%
  margin: 0 auto
</style>
