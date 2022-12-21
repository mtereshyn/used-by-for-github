<template>
  <div class="used-by">
    <used-by-form @request="request" />

    <div v-for="(user, index) in usedUserList" :key="index">
      <p>{{ user.name }}</p>
      <p>{{ user.star }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const cheerio = require("cheerio");

import UsedByForm from "@/Forms/UsedByForm";

export default {
  name: "used-by",

  components: {
    UsedByForm,
  },

  data() {
    return {
      usedUserList: [],
      link: "",
      usedList: [
        {
          name: "",
          stars: "",
        },
      ],
      isError: false,
    };
  },

  methods: {
    request(passRepoLink) {
      this.link = passRepoLink;
      this.link = this.link.replace(
        "https://github.com",
        "http://localhost:8080"
      );
      axios
        .get(this.link)
        .then((response) => {
          let htmlData = response;
          const $ = cheerio.load(htmlData.data);

          this.usedUserList = $(".Box-row")
            .map((index, user) => {
              const users = $(user).find("span.f5");
              const stars = $(user).find("span.text-bold").first();
              return {
                name: users.text().replace(/\s\s+/g, ""),
                star: stars.text().replace(/\s\s+/g, ""),
              };
            })
            .toArray();
          console.log(this.usedUserList);
        })
        .catch((error) => {
          console.log(error);
          this.isError = true;
        });
    },
  },
};
</script>
