<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-transparent">
    <router-link class="navbar-brand" :to="{ name: 'Home' }">
      <span class="localReach">localReach</span>
    </router-link>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarText"
      aria-controls="navbarText"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarText">
      <ul class="navbar-nav mr-auto">
        <li class="nav-item" :class="{ active: $route.name == 'Welcome' }">
          <router-link class="nav-link" :to="{ name: 'Welcome' }">Welcome</router-link>
        </li>
        <!-- <li class="nav-item mt-2">|</li> -->
        <li
          class="nav-item"
          v-if="$auth.isAuthenticated"
          :class="{ active: $route.name == 'Home' }"
        >
          <router-link :to="{ name: 'Home' }" class="nav-link">| Home</router-link>
        </li>
        <!-- <li class="nav-item mt-2">|</li> -->
        <li
          class="nav-item"
          v-if="$auth.isAuthenticated"
          :class="{ active: $route.name == 'Profile' }"
        >
          <router-link class="nav-link" :to="{ name: 'Profile' }">| Profile</router-link>
        </li>
        <!-- <li class="nav-item mt-2">|</li> -->
        <li
          class="nav-item"
          v-if="$auth.isAuthenticated"
          :class="{ active: $route.name == 'AddOrg' }"
        >
          <router-link :to="{ name: 'AddOrg' }" class="nav-link">| Organization</router-link>
        </li>
      </ul>

      <span class="navbar-text">
        <button class="btn btn-success" @click="login" v-if="!$auth.isAuthenticated">Login</button>
        <button class="btn btn-danger" @click="logout" v-else>logout</button>
      </span>
    </div>
  </nav>
</template>

<script>
import axios from "axios";
import { getUserData } from "@bcwdev/auth0-vue";
export default {
  name: "Navbar",
  methods: {
    async login() {
      await this.$auth.loginWithPopup();
      this.$store.dispatch("setBearer", this.$auth.bearer);
      console.log("this.$auth.user: ");
      console.log(this.$auth.user);
      this.$store.dispatch("getProfile");
    },
    async logout() {
      this.$store.dispatch("resetBearer");
      await this.$auth.logout({ returnTo: window.location.origin });
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Pacifico&display=swap");

.localReach {
  font-family: "Pacifico", cursive;
}
</style>
