<template>
  <button class="app-button" v-bind="$attrs" v-on="$listeners"><slot /></button>
</template>

<script>
export default {
  name: "app-button",
};
</script>
