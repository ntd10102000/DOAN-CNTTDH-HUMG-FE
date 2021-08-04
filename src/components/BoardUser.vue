<template>
  <div class="container">
    <header class="jumbotron">
      <ul id="example-1">
        <li v-for="(con, index) in content" :key="index">
          <h3 v-if="con != null">
            <router-link :to="'/showmaps/' + con.f_table_name">
              {{ con.f_table_name }}
            </router-link>
          </h3>
        </li>
      </ul>
      <form action="/profile" method="post" enctype="multipart/form-data">
        Chon file:
        <input
          type="file"
          name="shp"
          class="form-control btn-danger"
          multiple="multiple"
        />
        <button class="btn btn-danger">Import</button>
      </form>
    </header>
  </div>
</template>

<script>
import UserService from "../services/user.service";

export default {
  name: "User",
  data() {
    return {
      content: [],
    };
  },
  mounted() {
    UserService.getUserBoard().then(
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
  },
};
</script>