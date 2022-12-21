<template>
  <div class="used-by-form">
    <form class="used-by-form__form" @submit.prevent>
      <input-field
        v-model="reposLink"
        :placeholder="'Insert the github repository link'"
        class="used-by-form__input"
        size="40"
      />
      <app-button class="used-by-form__button" @click="request">
        Search
      </app-button>
    </form>
  </div>
</template>

<script>
import InputField from "@/Fields/InputField";
import AppButton from "@/Common/AppButton";

export default {
  name: "used-by-form",
  components: {
    InputField,
    AppButton,
  },

  data() {
    return {
      reposLink: "",
    };
  },
  methods: {
    request() {
      this.$emit("request", this.reposLink);
    },
  },
};
</script>

<style lang="sass">
.used-by-form
  margin-bottom: 2rem
  &__form
    display: flex
    align-items: center
    justify-content: center
  &__button
    border: none
    background-color: #1c1e21
    color: #c4c4c4
    padding: 1rem
    font-size: .75rem
    line-height: 1rem
    font-weight: 400
    text-transform: uppercase
</style>
