<template>
  <div class="used-by">
    <div class="container">
      <h1>Used By List</h1>
      <used-by-form @request="request" />
      <used-by-list :sorted-list="sortedList" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
const cheerio = require("cheerio");

import UsedByForm from "@/Forms/UsedByForm";
import UsedByList from "@/Pages/UsedBy/UsedByList";

export default {
  name: "used-by",

  components: {
    UsedByForm,
    UsedByList,
  },
  computed: {
    sortedList() {
      return this.usedUserListAll.slice().sort((a, b) => b.star - a.star);
    },
  },
  data() {
    return {
      usedUserList: [],
      usedUserListAll: [],
      nextPageLink: "",
      link: "",
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
        .then(async (response) => {
          let htmlData = response;
          const $ = cheerio.load(htmlData.data);
          await new Promise((resolve) => setTimeout(resolve, 500));
          this.usedUserList = $(".Box-row")
            .map((index, user) => {
              const users = $(user)
                .find(".f5 > a.text-bold")
                .attr("href")
                .replace(/\s\s+/g, " ");
              const userImage = $(user).find("img.avatar").attr("src");
              const stars = $(user).find("span.text-bold").first();
              return {
                name: users,
                star: stars.text().replace(/\s\s+/g, ""),
                avatar: userImage,
              };
            })
            .toArray();
          this.nextPageLink = $(".paginate-container > .BtnGroup")
            .children("a")
            .last()
            .attr("href");

          if (this.usedUserList.length >= 1) {
            this.request(this.nextPageLink);
            this.usedUserListAll.push(...this.usedUserList);
          }
          console.log(this.sortedList);
        })
        .catch((error) => {
          console.log(error);
          this.isError = true;
        });
    },
  },
};
</script>

<style lang="sass">
.used-by
  padding: 2rem 0
  h1
    text-align: center
    text-transform: uppercase
    margin-bottom: 1rem
    color: #c4c4c4
.container
  padding: 0 5rem
  margin: 0 auto
</style>
