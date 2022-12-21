<template>
  <div class="input-field">
    <input
      :value="value"
      v-bind="$attrs"
      v-on="listeners"
      :placeholder="placeholder"
      class="input-field__input"
    />
    <span class="input-field__error">
      {{ errorMessage }}
    </span>
  </div>
</template>

<script>
const EVENTS = {
  input: "input",
};

export default {
  name: "input-field",
  props: {
    value: {
      type: String,
      default: "",
    },
    placeholder: {
      type: String,
      default: "",
    },
    errorMessage: {
      type: String,
      default: "",
    },
  },
  data() {
    return {
      EVENTS,
    };
  },
  computed: {
    listeners() {
      return {
        input: (event) => {
          this.$emit(EVENTS.input, event.target.value);
        },
      };
    },
  },
};
</script>

<style lang="sass">
.input-field__input
  border: none
  padding: 1rem 1rem 1rem .5rem
  font-size: .75rem
  line-height: 1rem
  font-weight: 400
  background-color: #1c1e21
  color: #c4c4c4
  -webkit-appearance: none
  -moz-appearance: none
  appearance: none
.input-field__input::placeholder
  color: #c4c4c4
  text-transform: uppercase
</style>
