<template>
  <div class="used-by-form">
    <form class="used-by-form__form" @submit.prevent>
      <input-field
        v-model="reposLink"
        :placeholder="'Insert the github repository link'"
      />
      <app-button class="used-by-form__button" @click="request">
        Search
      </app-button>
    </form>
    <app-button>Clear</app-button>
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
