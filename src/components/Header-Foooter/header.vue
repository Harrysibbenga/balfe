<template>
  <b-navbar toggleable="true" type="dark" variant="dark">
    <b-navbar-brand to="/">
      <img class="img-fluid logo" src="../../assets/Balfe_logo.png" />
    </b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <!-- Right aligned nav items -->
      <b-navbar-nav class="mx-auto align-items-center">
        <!-- Links -->
        <b-nav-item href="#">News</b-nav-item>
        <b-nav-item href="#media-sec">Media</b-nav-item>
        <b-nav-item href="#drivers-sec">Drivers</b-nav-item>
        <b-nav-item href="#calender">Calender</b-nav-item>
        <b-nav-item href="#partners-sec">Partners</b-nav-item>
        <b-nav-item href="#">History</b-nav-item>
        <b-nav-item v-if="!currentUser" to="/login">Login</b-nav-item>
        <b-nav-item v-if="currentUser" @click="logout">Logout</b-nav-item>
        <b-nav-item to="/dashboard" v-if="currentUser">Dashboard</b-nav-item>
        <!-- Links -->
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</template>

<script>
const fb = require("../../firebaseConfig");

export default {
  computed: {
    currentUser() {
      return this.$store.getters["admin/currentUser"];
    }
  },
  methods: {
    logout() {
      fb.auth.signOut().then(() => {
        this.$store.dispatch("admin/clearData");
        this.$router.push("/");
      });
    }
  }
};
</script>
