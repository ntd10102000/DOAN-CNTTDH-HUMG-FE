<template>
  <div class="container">
    <header class="jumbotron">
      <h1 id="s" style="display: none;">{{ name }}</h1>
      <h3>{{ content }}</h3>
    </header>
  </div>
</template>

<script>
var s;
import UserService from "../services/user.service";

export default {
  name: "Admin",
  props: ["name"],
  data() {
    return {
      content: "",
    };
  },
  async mounted() {
    await setTimeout(async () => {
      s = await document.getElementById("s").innerHTML;
      await UserService.getUserData(s).then(
        (response) => {
          this.content = response.data;
        },
        (error) => {
          this.content =
            (error.response &&
              error.response.data &&
              error.response.data.message) ||
            error.message ||
            error.toString();
        }
      );
    }, 1000);
  },
};
</script>