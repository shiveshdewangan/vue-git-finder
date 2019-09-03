<template>
    <Users />
</template>

<script>
import Vue from 'vue'
import BootstrapVue from 'bootstrap-vue'
import Users from "./components/users.vue";
import './styles/style.css';

export default {
  name: "users",
  components: {
    Users
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Lato&display=swap');
</style>