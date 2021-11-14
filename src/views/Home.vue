<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <table width="100%">
      <tr>
        <td>User Name</td>
        <td><input type="text" v-model="username" /></td>
      </tr>
      <tr>
        <td>Password</td>
        <td><input type="password" v-model="password" /></td>
      </tr>
      <tr>
        <button @click="login()">Login</button>
      </tr>
    </table>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import VueAxios from "vue-axios";
Vue.use(VueAxios, axios);

export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    login() {
      axios
        .post(
          "https://localhost:44301/login",
          {},
          {
            auth: {
              username: this.username,
              password: this.password,
            },
          }
        )
        .then((response) => {
          console.log(response.data["token"]);
           localStorage.setItem('token', response.data["token"])
        })
        .catch(() => console.log("login fail"));
    },
  },
};
</script>

<style>
</style>