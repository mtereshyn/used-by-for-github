<template>
  <div class="input-field">
    <div class="input-field__input-wrapper">
      <input
        :value="value"
        v-bind="$attrs"
        v-on="listeners"
        :placeholder="placeholder"
        class="input-field__input"
      />
    </div>
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
