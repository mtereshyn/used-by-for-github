<template>
  <div id="app">
    <input type="text" v-bind="$attrs" v-model="reposLink" />

    <button type="submit" @click="request()">Search</button>
  </div>
</template>

<script>
import axios from "axios";
const cheerio = require("cheerio");

export default {
  name: "App",
  data() {
    return {
      usedByUserList: [],
      linkForGitHub: "",
      reposLink: "",
    };
  },
  methods: {
    request() {
      if () {
        axios
          .get(
            `http://localhost:8080/${this.nameOfUser}/${this.nameOfRepos}/network/dependents`
            //https://github.com/npm/cli/network/dependents?dependents_before=MjYwMDE2MjcyOTk
          )
          .then((response) => {
            let htmlData = response;
            const $ = cheerio.load(htmlData.data);
            this.usedByUserList = $("div.Box-row");
            this.usedByUserList
              .each((index, element) => {
                const user = $(element)
                  .find(".f5")
                  .text()
                  .replace(/\s\s+/g, " ");
                const avatar = $(element)
                  .find("img")
                  .attr("src")
                  .replace(/\s\s+/g, "");

                console.log(user + "\n" + avatar);
                return { user: user, avatar: avatar };
              })
              .toArray();
          });
      }
    },
  },
};
</script>

<style lang="scss">
.list {
  display: flex;
}
</style>
