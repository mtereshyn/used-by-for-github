<template>
  <div id="app">
    <used-by />
  </div>
</template>

<script>
import UsedBy from "@/Pages/UsedBy";
export default {
  name: "app",
  components: {
    UsedBy,
  },
};
</script>

<style lang="scss">
.list {
  display: flex;
}
</style>
