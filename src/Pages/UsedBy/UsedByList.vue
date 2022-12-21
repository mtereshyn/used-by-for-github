<template>
  <ul class="used-by-list">
    <used-by-item
      v-for="(user, index) in sortedList"
      :key="index"
      :user="user"
    />
  </ul>
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
  },
};
</script>

<style lang="sass">
.used-by-list
  list-style: none
  display: flex
  flex-direction: column
  align-items: center
  gap: 1rem
  max-width: 70%
  margin: 0 auto
</style>
